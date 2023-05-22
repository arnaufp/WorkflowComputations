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

```json
"return JToken.FromObject(Variables.ids).ToString();"

{
  "singleValue": [],
  "allValues": {}
}
```

```json
"return JToken.FromObject(Variables.ids.SingleValue).ToString();"

[]
```
Linq methods could be then used, such as for example:

"Variables.ids.SingleValue.Count();" ==> 0

"JToken.FromObject(Variables.ids.SingleValue.First()).ToString();" ==> ERROR

### For nodes outputing items

```json
"return JToken.FromObject(Variables.ids).ToString();"

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

```json
"return JToken.FromObject(Variables.ids.SingleValue).ToString();"

[
  "645ce1a84d51bf0367bfce3e",
  "62baddbf44501301c83a252a"
]
```
Linq methods could be then used, such as for example:

"Variables.ids.SingleValue.Count();" ==> 2

"JToken.FromObject(Variables.ids.SingleValue.First()).ToString();" ==> "645ce1a84d51bf0367bfce3e"

etc...
