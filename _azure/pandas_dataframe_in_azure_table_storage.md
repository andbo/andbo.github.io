---
layout: page
title:  "Pandas DataFrame in Azure Table Storage"
categories: azure
permalink: /azure/pandas_dataframe_in_azure_table_storage/
---
Here is a take on how to store Pandas DataFrame in Azure Table Storage.
The DataFrame used here consists of time values the time values are not necessarily evenly distributed.
The storing DataFrames in Azure Table Storage is meant for the case where you have too much data to have it all in one DataFrame.
And need your data to be consumable by others or other applications.

## Setup

This assumes you have [conda](https://conda.io/miniconda.html) installed.
Create a new [conda environment](https://conda.io/docs/user-guide/tasks/manage-environments.html):
{% highlight posh %}
conda create -n py36azure python=3.6 anaconda python-blosc azure
{% endhighlight %}

Create an Azure Storage Account either via the web interface or via the the [Python module](https://azure.microsoft.com/en-us/resources/samples/storage-python-manage/) or one of the other methods for creating a storage account. Remember to create a general purpose storage account not a blob only storage account else you wont have the Azure Table Storage.

## Azure Table Storage


## Inserting DataFrame


### Transforming the DataFrame
Transforming data frame into dicts

### Compression
If the limit
