# Check IDs + ternary conditional + string interpolation

Often you need to send an item id as part of an HTTP requests (e.g. service enquiry with an outcome link). In variables you get items ids in an array which can have 0 or more ids.
When 0 string must be empty, while when 1 string must be the item id in index 0 of the array. 
In these cases string interpolation becomes very useful as you do not need to access the WFC Variables syntax e.g. JToken.FromObject(Variables.itemIds.SingleValue).ToString()

<br/>

```json
{
      "name": "outcomeIds",
      "value": {
        "outputAction": "67add1718b2ef8de72609198",
        "itemValue": {
          "property": "ItemId",
          "discriminator": "WorkflowSyntaxArgumentItemValueItemPropertyWebModel"
        },
        "outputMode": "All",
        "discriminator": "WorkflowSyntaxNodeOutputWebModel"
      }
    },
    {
      "name": "outcome",
      "value": {
        "script": "return outcomeIds.Count() > 0 ? $\"{outcomeIds[0]}\" : \"\";",
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
      }
    }
```
