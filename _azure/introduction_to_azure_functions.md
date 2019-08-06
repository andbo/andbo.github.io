---
layout: slide
title:  "Introduction to Azure Functions"
excerpt: "A presentation by abbo"
theme: solarized
#theme: black
transition: slide # "default”, “fade”, “slide”, “convex”, “concave”, “zoom” or “none”.
categories: azure
permalink: /azure/introduction_to_azure_functions/
baseurl: /azure/
---
<section data-markdown>
# Introduction to Azure Functions
</section>

<section data-markdown>
## TOC
- Cloud First
- Serverless Computing
- Microsoft Azure Functions
</section>


<section data-markdown data-separator-vertical="--">
## Cloud First
 - Infrastructure as a Service (IaaS)
 - Platform as a Service (PaaS)
 - Software as a Service ([SaaS](https://azure.microsoft.com/en-us/overview/what-is-saas/ 'What is SaaS'))

--
## Infrastructure as a Service (IaaS)
 - Data center physical plant/building
 - Networking firewalls/security
 - Servers and storage
--
## Platform as a Service (PaaS)
 - Operation systems
 - Development tools
 - Database management
 - Business analytics

--
## Software as a Service (SaaS)
 - Hosted applications/apps

</section>

<section data-markdown data-separator-vertical="--">
## Serverless Computing
 - Storage as a Service (SaaS)
 - Function as a Service (FaaS)

--
## Storage as a Service (SaaS)
 - Also known as Cloud Storage
 - Started in 2006 by AWS S3
 - SaaS is now referring to Software as a Service
--
## Function as a Service (FaaS)
- The new black within cloud computing (2014)
  - AWS Lambda
  - Google Cloud Functions
  - Microsoft Azure Functions (2016)
- For developers thus not mentioned by Vattenfall IT:)
</section>



<section data-markdown data-separator-vertical="--">
## What is a function
 - Piece of code
 - Triggered by something
 - Can take in other inputs
 - To generated the wanted output

--
### Programming languages
 - Bash, Batch, PowerShell
 - **C#**, F#
 - **JavaScript**, **TypeScript** , PHP,
 - **Python**

--
### Triggers:
 - Schedule
 - HTTP
 - Blob Storage
 - Events, Queues

--
### Input
   - Blob Storage
   - Tables

--
### Output
   - HTTP
   - Blob Storage
   - Events, Queues
   - Tables
   - SMS, E-MAIL
</section>

<section data-markdown data-separator-vertical="--">
## Microsoft Azure Functions Cost
 - Billing is by GB-Seconds and by the number of request
 - Price after free package is used:
   - €0.000014/GB-S
   - €0.169 per million executions
--
## Included in a subscription
- 440,000 GB-S included
  - (My small test used 106.21 GB-S)
- 1,100,000 Request included
  - (My small test used 20)

</section>

<section data-markdown>
## Next steps
 - [Azure Functions Challenge](/azure/azure_functions_challenge)
 - [K thanks bye](/azure/)
</section>
