>## Get Datetimes attributes
```json
{
  "name": "datetimes",
  "value": {
    "outputAction": "645ce6e8f7339103742a032e",
    "itemValue": {
      "attributeCode": "attributes_tasksStartTime",
      "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
    },
    "discriminator": "WorkflowSyntaxNodeOutputWebModel"
  }
}
```
### For nodes not outputing items

```json
"return JToken.FromObject(Variables.datetimes).ToString();"

{
  "allValues": {}
}
```

```json
"return JToken.FromObject(Variables.datetimes.AllValues).ToString();"

{}
```

```json
"return JToken.FromObject(Variables.datetimes.AllValues.Values).ToString();"

[]
```

```json
"return JToken.FromObject(Variables.strings.AllValues.Values.Select(x => x.SingleValue)).ToString();"

[]
```

### For nodes outputing items, with the datetime attribute populated

```json
"return JToken.FromObject(Variables.datetimes).ToString();"

{
  "singleValue": "2023-05-22T02:00:00Z",
  "allValues": {
    "0": {
      "singleValue": "2023-05-22T02:00:00Z",
      "allValues": {
        "0": {
          "singleValue": "2023-05-22T02:00:00Z",
          "allValues": {}
        }
      }
    },
    "1": {
      "singleValue": "2023-05-22T02:00:00Z",
      "allValues": {
        "0": {
          "singleValue": "2023-05-22T02:00:00Z",
          "allValues": {}
        }
      }
    }
  }
}
```

```json
"return JToken.FromObject(Variables.datetimes.AllValues).ToString();"

{
  "0": {
    "singleValue": "2023-05-22T02:00:00Z",
    "allValues": {
      "0": {
        "singleValue": "2023-05-22T02:00:00Z",
        "allValues": {}
      }
    }
  },
  "1": {
    "singleValue": "2023-05-22T02:00:00Z",
    "allValues": {
      "0": {
        "singleValue": "2023-05-22T02:00:00Z",
        "allValues": {}
      }
    }
  }
}
```

```json
"return JToken.FromObject(Variables.datetimes.AllValues.Values).ToString();"

[
  {
    "singleValue": "2023-05-22T02:00:00Z",
    "allValues": {
      "0": {
        "singleValue": "2023-05-22T02:00:00Z",
        "allValues": {}
      }
    }
  },
  {
    "singleValue": "2023-05-22T02:00:00Z",
    "allValues": {
      "0": {
        "singleValue": "2023-05-22T02:00:00Z",
        "allValues": {}
      }
    }
  }
]
```

```json
"return JToken.FromObject(Variables.datetimes.AllValues.Values.Select(x => x.SingleValue)).ToString();"

[
  "2023-05-22T02:00:00Z",
  "2023-05-22T02:00:00Z"
]
```
### For nodes outputing items, without the datetime attribute populated

```json
"return JToken.FromObject(Variables.datetimes).ToString();"

{
  "allValues": {
    "0": {
      "allValues": {
        "0": {
          "allValues": {}
        }
      }
    },
    "1": {
      "allValues": {
        "0": {
          "allValues": {}
        }
      }
    }
  }
}
```


```json
"return JToken.FromObject(Variables.datetimes.AllValues).ToString();"

{
  "0": {
    "allValues": {
      "0": {
        "allValues": {}
      }
    }
  },
  "1": {
    "allValues": {
      "0": {
        "allValues": {}
      }
    }
  }
}
```


```json
"return JToken.FromObject(Variables.datetimes.AllValues.Values).ToString();"

[
  {
    "allValues": {
      "0": {
        "allValues": {}
      }
    }
  },
  {
    "allValues": {
      "0": {
        "allValues": {}
      }
    }
  }
]
```


```json
"return JToken.FromObject(Variables.datetimes.AllValues.Values.Select(x => x.SingleValue)).ToString();"

[
  null,
  null
]
```
