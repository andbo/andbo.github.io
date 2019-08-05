---
layout: page
title:  "Azure Functions Challenge"
categories: azure
permalink: /azure/azure_functions_challenge/
---
In this post I will go through my solution to the [Azure Functions Challenge](https://functionschallenge.azure.com/ 'Azure Functions Challenge').
I decided to use the Node.js for my solutions to challenge myself. Since the challenge does not proposed solution to all the questions in Node.js, I constructed this post.

## Ping? Pong!
As simple as it gets. Just create the default Webhook function and modify it a tiny bit.
### Challenge
- Input:
{% highlight json %}
{
  "ping": "64daf138-9ae7-41fa-b2aa-b69efa0218e0"
}
{% endhighlight %}
- Expected Output:
{% highlight json %}
{
  "pong": "64daf138-9ae7-41fa-b2aa-b69efa0218e0"
}
{% endhighlight %}

### Solution
{% highlight js %}
module.exports = function (context, data) {
  context.log('Webhook was triggered!');
  // Check if we got a ping
  if ('ping' in data) {
    context.res = {
      body: { pong: data.ping }
    };
  } else {
    context.res = {
      status: 400,
      body: { error: 'Please pass a ping to get a pong'}
    };
  }
  context.done();
}
{% endhighlight %}

## Decipher Text

### Challenge

- Input:
{% highlight json %}
{
  "key": "2588afea-027f-4093-a0e0-79e25923d614",
  "msg": "3919158618333218751586927582881532861062862782398627102415",
  "cipher": {"a":56,"b":20,"c":24,"d":85,"e":15,"f":92,"g":25,"h":19,"i":10,"j":66,"k":83,"l":75,"m":73, "n":27,"o":82,"p":18,"q":71,"r":32,"s":62,"t":39,"u":33,"v":64,"w":88,"x":54,"y":95,"z":35," ":86
  }
}
{% endhighlight %}

 - Expected output:
{% highlight json %}
{
  "key": "2588afea-027f-4093-a0e0-79e25923d614",
  "result": "the purple flower is not nice"
}
{% endhighlight %}

### Solution

{% highlight js %}
function val2key(val, array) {
  for (var key in array) {
    this_val = array[key];
    if (this_val == val) {
      return key;
      break;
    }
  }
}

module.exports = function (context, data) {
  context.log('Webhook was triggered!');
  if ('key' in data && 'msg' in data && 'cipher' in data) {
    var msgText = data.msg;
    var cipher = data.cipher;
    var result = "";
    // Decode the Message by using the Cipher
    var real_keys = data.msg.match(/.{1,2}/g)
    for (k of real_keys) {
      result += val2key(k, cipher)
    }

    context.res = {
      key: data.key,
      result: result
    };
  } else {
    context.res = {
      status: 400,
      body: { error: 'Please pass key,msg, and cipher'}
    };
  }
  context.done();
}
{% endhighlight %}

## Sort Array
### Challenge
This challenge is a bit different from the others and is presented as a two step challenge.
#### Step 1
- Input:
{% highlight json %}
{
  "key": "1b189de1-5c68-49ab-aa3b-5a6c0835ea7d",
  "ArrayOfValues": [95,45,34,3,700,...	]
}
{% endhighlight %}
 - Output:
{% highlight json %}
{}
{% endhighlight %}
#### Step 2
 - Input:
{% highlight json %}
{
  "key": "1b189de1-5c68-49ab-aa3b-5a6c0835ea7d"
}
{% endhighlight %}
 - Output:
{% highlight json %}
{
  "key": "1b189de1-5c68-49ab-aa3b-5a6c0835ea7d",
  "ArrayOfValues": [3,34,45,95,700,...	]
}
{% endhighlight %}
### Solution
Even with the challenge being more complex than the others the solution is still simple and short.
So instead of splitting the solution up into two functions I merge it into one.
{% highlight js %}
module.exports = function (context, data) {
  context.log('Webhook was triggered!');
  context.bindings.outputTable = []
  context.log(data);
  // Step 1
  if ('key' in data && 'ArrayOfValues' in data) {
    context.res = {
      body: {}
      };
    context.bindings.outputTable.push({
      PartitionKey: "Test",
      RowKey: data.key,
      ArrayOfValues: data.ArrayOfValues
      });
  }
  // Step 2
  else if ('key' in data) {
    function findKey(dat) {
      return dat.RowKey == data.key;
    }
    result = context.bindings.inputTable.find(findKey)
    context.res = {
      body: {
        key: result.RowKey,
        ArrayOfValues: JSON.parse(result.ArrayOfValues).sort(function (a, b) { return a - b })
      }
    };
  } else {
    context.res = {
      status: 400,
      body: { error: 'Please pass key/ArrayOfValues' }
    };
  }
  context.done();
}
{% endhighlight %}

{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
      "name": "req"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "res"
    },
    {
      "type": "table",
      "name": "outputTable",
      "tableName": "challengeSortArray",
      "connection": "scadafunctions_STORAGE",
      "direction": "out"
    },
    {
      "type": "table",
      "name": "inputTable",
      "tableName": "challengeSortArray",
      "take": 50,
      "connection": "scadafunctions_STORAGE",
      "direction": "in",
      "partitionKey": "Test"
    }
  ],
  "disabled": false
}


## Github Deploy

Press the button.
