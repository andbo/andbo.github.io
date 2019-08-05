---
layout: page
title:  "Installing Python on Azure Functions"
categories: azure
permalink: /azure/installing_python_on_azure_functions/
---
This is a brief overview how to install Python3 and some modules on Azure functions.

## Installing Python
Azure functions come with Python as a default but it is Python 2.7 and that should not be used for any new code so first step is to install Python3.

### Nuget install

First step to install the Nuget package for Python is to find the latest version available at [Site Extensions](https://www.siteextensions.net/packages?q=python3 'Python3 Site Extension Search').
{% highlight posh %}
nuget.exe install -Source https://www.siteextensions.net/api/v2/ -OutputDirectory D:\home\site\tools python361x64
{% endhighlight %}

### Move it
{% highlight posh %}
mv /d/home/site/tools/python361x64.3.6.1.3/content/python361x64/* /d/home/site/tools/
{% endhighlight %}


[Nice blog post about this topic](https://prmadi.com/running-python-code-on-azure-functions-app/)

### Install a Python Module
{% highlight posh %}
D:\home\site\tools\python.exe -m pip install pandas  
{% endhighlight %}
