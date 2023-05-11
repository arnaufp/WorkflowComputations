# Output Variables: returns

Output Variables return different types of elements depending on whether you want item ids or whether you want string, number, datetime... attributes or whether the output node does not output any item
The goal of this page is to try to list what you will get when using output variables in any of the combinations mentioned above.

>## Get Item Ids
```json
{
  "name": "ids",
  "value": {
    "outputAction": "645cc41e87557f0373bae7a1",
    "itemValue": {
      "property": "ItemId",
      "discriminator": "WorkflowSyntaxArgumentItemValueItemPropertyWebModel"
    },
    "discriminator": "WorkflowSyntaxNodeOutputWebModel"
  }
}
```
### For nodes not outputing items
"return JToken.FromObject(**Variables.ids**).ToString();"
```json
{
  "singleValue": [],
  "allValues": {}
}
```
"return JToken.FromObject(**Variables.ids.SingleValue**).ToString();"
```json
[]
```
Linq methods could be then used, such as for example:

"Variables.ids.SingleValue.Count();" ==> 0

"JToken.FromObject(Variables.ids.SingleValue.First()).ToString();" ==> ERROR

### For nodes outputing items
"return JToken.FromObject(**Variables.ids**).ToString();"
```json
{
  "singleValue": [
    "645ce1a84d51bf0367bfce3e",
    "62baddbf44501301c83a252a"
  ],
  "allValues": {
    "0": {
      "singleValue": [
        "645ce1a84d51bf0367bfce3e"
      ],
      "allValues": {
        "0": {
          "singleValue": [
            "645ce1a84d51bf0367bfce3e"
          ],
          "allValues": {}
        }
      }
    },
    "1": {
      "singleValue": [
        "62baddbf44501301c83a252a"
      ],
      "allValues": {
        "0": {
          "singleValue": [
            "62baddbf44501301c83a252a"
          ],
          "allValues": {}
        }
      }
    }
  }
}
```
"return JToken.FromObject(**Variables.ids.SingleValue**).ToString();"
```json
[
  "645ce1a84d51bf0367bfce3e",
  "62baddbf44501301c83a252a"
]
```
Linq methods could be then used, such as for example:

"Variables.ids.SingleValue.Count();" ==> 2

"JToken.FromObject(Variables.ids.SingleValue.First()).ToString();" ==> "645ce1a84d51bf0367bfce3e"

etc...

<br/>
<br/>

>## Get Number attributes
```json
{
  "name": "numbers",
  "value": {
    "outputAction": "645ce6e8f7339103742a032e",
    "itemValue": {
      "attributeCode": "attributes_jobWorkItemsEstimatedCost",
      "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
    },
    "discriminator": "WorkflowSyntaxNodeOutputWebModel"
  }
}
```
### For nodes not outputing items
"return JToken.FromObject(**Variables.numbers**).ToString();"
```json
{
  "allValues": {}
}
```
"return JToken.FromObject(**Variables.numbers.AllValues**).ToString();"
```json
{}
```
"return JToken.FromObject(**Variables.numbers.AllValues.Values**).ToString();"
```json
[]
```
"Variables.numbers.AllValues.Values.Sum(x => x.SingleValue);" ==> 0

### For nodes outputing items
"return JToken.FromObject(**Variables.numbers**).ToString();"
```json
{
  "singleValue": 1.5,
  "allValues": {
    "0": {
      "singleValue": 1.5,
      "allValues": {
        "0": {
          "singleValue": 1.5,
          "allValues": {}
        }
      }
    },
    "1": {
      "singleValue": 2.4,
      "allValues": {
        "0": {
          "singleValue": 2.4,
          "allValues": {}
        }
      }
    }
  }
}
```
"return JToken.FromObject(**Variables.numbers.AllValues**).ToString();"
```json
{
  "0": {
    "singleValue": 2.4,
    "allValues": {
      "0": {
        "singleValue": 2.4,
        "allValues": {}
      }
    }
  },
  "1": {
    "singleValue": 1.5,
    "allValues": {
      "0": {
        "singleValue": 1.5,
        "allValues": {}
      }
    }
  }
}
```
"return JToken.FromObject(**Variables.numbers.AllValues.Values**).ToString();"
```json
[
  {
    "singleValue": 2.4,
    "allValues": {
      "0": {
        "singleValue": 2.4,
        "allValues": {}
      }
    }
  },
  {
    "singleValue": 1.5,
    "allValues": {
      "0": {
        "singleValue": 1.5,
        "allValues": {}
      }
    }
  }
]
```
"Variables.numbers.AllValues.Values.Sum(x => x.SingleValue);" ==> 3.9
