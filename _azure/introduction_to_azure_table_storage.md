---
layout: slide
title:  "Introduction to Azure Table Storage"
title_slide: true
excerpt: "A presentation at the 2016 Archive-It Partner Meeting, focusing on automating the QA workflow to minimize costs by utilizing student employees"
theme: solarized
#theme: black
transition: default # "default”, “fade”, “slide”, “convex”, “concave”, “zoom” or “none”.
categories: azure
permalink: /azure/introduction_to_azure_table_storage/
baseurl: /azure/
---

<section data-markdown>
# Introduction to Azure Table Storage
Anders Bech Borchersen
</section>

<section data-markdown>
![get a better browser](../giphy_foot.gif)
</section>

<section data-markdown>
## TOC
- Motivation
- Azure Table storage
- SCADA data in Azure
- Table Storage for SCADA
</section>

<section data-markdown data-separator-vertical="^---$">
## Uses cases for Azure
  - SCADA
    - Reporting (Wind Web Portal)
    - Data validation and quality ensures
    - Mobile application
  - Others
    - R&D and Data Analysis
    - Sharing with externals
---
## Azure Storage
 - **Blob** and Archive
 - **Table** and Queue
 - File and Disk

---
 | **Blob** |  | Archive
 |:--------|:-------:|:--------|
 | Cost-effective for massive volume | | Data automatically encrypted at rest |
 | Tiered storage options | | Seamless integration with hot and cool storage tiers |
 | Single infrastructure with global reach | | Supported by leading Data Management partners |

---
 | **Table** |  | Queue
 |:--------|:-------:|:--------|
 | Key-value table storage | | Simple, cost-effective messaging |
 | Structured or unstructured data | | Decoupled component flexibility |
 | Low latency at Internet scale | |  Resilient scaling and buffering |

---
| File |  | Disk
|:--------|:-------:|:--------|
| Lift and shift migration  | | Low latency, high throughput |
| Simple and inexpensive  | | Automatic triple replication |
| Move data to cloud with no coding | | Enterprise-grade durability |

</section>

<section data-markdown data-separator-vertical="^---$">
## Azure Table Storage
  * Cheap, Scalable, NoSQL key-value store
  * Libraries (.NET, Java, Node.js, **Python**, Golang, Ruby)
  * Rest API and OData via HTTP/HTTPS
  * Integrated with Azure Functions

---
### Price
| Capacity | LRS [GB/month] | GRS [GB/month] | RA-GRS [GB/month]
|:------------|:-----:|:------:|:------:|
| 1 TB | €0.0591 | €0.0802 | €0.1012 |
| 50 TB | €0.0549 | €0.0675 | €0.0844 |
| 500 TB | €0.0506 | €0.0591 | €0.0759 |
| 1000 TB | €0.0464 | €0.0549 | €0.0675 |
| 5000 TB | €0.0380 | €0.0506 | €0.0633 |

€0.000304 per 10,000 transactions for tables
---
### Azure Storage Price
![get a better browser](../azure_storage_price.svg)
---
### Log log plot
![get a better browser](../azure_storage_price_loglog.svg)
</section>

<section data-markdown>
<script type="text/template">
### The No in NoSQL
- No schema <!-- .element: class="fragment" data-fragment-index="1" -->
- No join <!-- .element: class="fragment" data-fragment-index="1" -->
- No stored procedures <!-- .element: class="fragment" data-fragment-index="2" -->
- No custom index <!-- .element: class="fragment" data-fragment-index="2" -->
- No size limits (500 TB) <!-- .element: class="fragment" data-fragment-index="3" -->
- No "hardware" <!-- .element: class="fragment" data-fragment-index="3" -->
- No fixed cost <!-- .element: class="fragment" data-fragment-index="3" -->

![get a better browser](../giphy_ni.gif) <!-- .element: class="fragment" data-fragment-index="3" -->
</script>
</section>


<section data-markdown data-separator-vertical="^---$">
## Designing an Azure Table Storage
  - Define uses cases
    1. How should it scale
    1. What will your "normal" queries look like
    1. What information is needed
  - Then you design your table storage:
    1. PartitionKey
    1. RowKey
    1. Entity properties

---
### PartitionKey and RowKey
  - Together they must be unique
  - Scale out is done using the PartitionKey
  - Search speed
    1. Point Query: PartitionKey, RowKey
    1. Range Query: PartitionKey, filter on RowKey
    1. Partition Scan: PartitionKey, filter on property
    1. Table Scan: Filter on Rowkey
    1. Table Scan: Filter on property

---
### Entity
 - Consist of PartitionKey, RowKey and Properties
 - Max size of a table entity	1 MB
 - Max number of properties in a table entity	252
 - Max size of a single property 64 KB
</section>



<section data-markdown data-separator-vertical="^---$">
## SCADA data in Azure
  - The flow of SCADA data
  - The structure of SCADA data and time series data
  - Use cases for SCADA data

---
## Flow of SCADA to Azure
![Alt text](../turbine_to_azure.svg)

---
## SCADA Time Series
```csv
Time(UTC)[YYYY-MM-DD hh:mm:ss.ssssss],WH1101-ActivePower(Aktuel produktion (sec))[kW]
2007-01-13 00:00:13.328003,1998.699951171875
2007-01-13 00:00:23.359009,2003.5
2007-01-13 00:00:33.312012,1992.199951171875
2007-01-13 00:00:43.389999,2007.4000244140625
2007-01-13 00:00:53.375000,1999.4000244140625
2007-01-13 00:01:03.343002,1995.699951171875
2007-01-13 00:01:13.343002,1998.5
2007-01-13 00:01:23.234009,1996.5999755859375
2007-01-13 00:01:33.406006,2009.300048828125
2007-01-13 00:01:53.375000,1999.9000244140625
2007-01-13 00:02:03.389999,2004.5999755859375
2007-01-13 00:02:13.375000,2003.5999755859375
2007-01-13 00:02:23.389999,1992.0999755859375
2007-01-13 00:02:33.389999,2005.800048828125
2007-01-13 00:02:43.343002,2007.9000244140625
2007-01-13 00:02:53.359009,2004.4000244140625
2007-01-13 00:03:03.389999,2007.0
2007-01-13 00:03:13.421005,1995.300048828125
2007-01-13 00:03:33.296005,1998.5999755859375
2007-01-13 00:03:43.359009,2008.5999755859375
...
2007-01-13 15:42:26.468002,1445.4000244140625
2007-01-13 15:42:36.515015,1510.800048828125
2007-01-13 15:42:46.484009,1394.4000244140625
2007-01-13 15:42:56.500000,1476.199951171875
2007-01-13 15:43:06.093002,1524.0
2007-01-13 15:43:16.484009,1481.699951171875
2007-01-13 15:43:26.515015,1523.800048828125
2007-01-13 15:43:36.468002,1462.699951171875
2007-01-13 15:43:46.468002,1434.5
2007-01-13 15:43:56.468002,1556.4000244140625
2007-01-13 15:44:16.500000,1570.5
```
---
## Use cases
  - Reporting (Wind Web Portal)
  - Data validation and quality ensures
  - Mobile application
  - Data Analysis
  - R&D
  - Trading
  - External third parties

---
## Requirements
  - Data available in different resolutions
    - (1 hour, 10 minute, 5 minute, raw values)
  - Easy consumable
    - REST (OData), Python, C#
  - Detailed user access control
  - Fast extraction of long time series
  - "Real time" data
</section>

<section data-markdown data-separator-vertical="^---$">
## Table storage for SCADA

![Alt text](../csv_to_azure.svg)
---
## Table Storage for SCADA
  - Multiple data points per entity (1 hour)
  - PartionKey: Turbine id + tag
    - WH1101_ActivePower
  - RowKey: Start time as %Y%m%d_%H%M%S
    - 20070113_000000
    - 20070113_150000

---
## Properties
  - Calculated values
  - Raw values
  - Time stamp

```python
d["PartitionKey"] = gr.keys()[0].split("(")[0].replace("-","_")
d["RowKey"] = idx.to_pydatetime().strftime("%Y%m%d_%H%M%S")
d["startTime"] = idx.to_pydatetime()
d["endTime"] = idx.to_pydatetime() + pd.Timedelta(split_freq)
d["count"] = len(gr)
d["mean"] = float(np.mean(gr))
d["min"] = float(np.min(gr))
d["max"] = float(np.max(gr))
d["std"] = float(np.std(gr))
```
---
## Raw Values
  - Binary object
  ```python
bin_index = np.array(gr.index, dtype="datetime64[ns]").tostring()
bin_values = np.array(gr, dtype=np.float64).tostring()
  ```
  - Compression
  ```python
  d["index"] = blosc.compress(bin_index, cname='zstd')
  d["values"] = blosc.compress(bin_values, cname='zstd')
  ```

---
## Index
  - No easy way of getting meta information
  - So a fake index is updated at every insert
  - PartionKey: index
  - RowKey: Turbine id + tag
    - WH1101_ActivePower
    - WH1101_WindSpeed
  - Properties:
    - startTime and endTime
    - unit, site name, etc. (not implemented yet)

---
## None Shall pass
![Get a better browser](../monty-python-stop.gif)

---
## SAS Token
  - Token generation via [Azure Functions](/azure/installing_python_on_azure_functions/)
  - Using the [table storage sdk](https://azure.github.io/azure-storage-python/ref/azure.storage.table.tableservice.html)

```python
from azure.storage.table import TableService, TablePermissions

table_service = TableService(account_name=acc_name,
                             account_key=acc_key)

generate_table_shared_access_signature(table_name,
                                       permission=None,
                                       expiry=None, start=None,
                                       id=None,
                                       ip=None, protocol=None,
                                       start_pk=None, end_pk=None,
                                       start_rk=None, end_rk=None)
```

</section>

<section data-markdown>
<script type="text/template">
## summary
  - Overview of SCADA data in Azure <!-- .element: class="fragment" data-fragment-index="1" -->
  - Fitting SCADA data in Azure Storage Table <!-- .element: class="fragment" data-fragment-index="1" -->
  - SCADA in Azure Table storage: <!-- .element: class="fragment" data-fragment-index="2" -->
    - One table for raw and aggregated data <!-- .element: class="fragment" data-fragment-index="3" -->
    - High performance compared to OSISoft PI <!-- .element: class="fragment" data-fragment-index="3" -->
    - Cheap and Scalable <!-- .element: class="fragment" data-fragment-index="3" -->
    - Detailed user management <!-- .element: class="fragment" data-fragment-index="3" -->
</script>
</section>

<section data-markdown data-separator-vertical="^---$">
## Questions?
![Get a better browser](../original_night.gif)

---
## Next steps
  - Try it out and give feedback
  - [Live Demo](https://scadapoc2.azurewebsites.net/api/tabletoken)
  - [K thanks bye](/azure/)

![Get a better browser](../giphy_falcon_heavy.gif)<!-- .element: class="fragment" fade-up -->
</section>
