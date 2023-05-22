>## Get Text attributes
```json
{
  "name": "strings",
  "value": {
    "outputAction": "645ce6e8f7339103742a032e",
    "itemValue": {
      "attributeCode": "attributes_tasksDescription",
      "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
    },
    "discriminator": "WorkflowSyntaxNodeOutputWebModel"
  }
}
```
### For nodes not outputing items

```json
"return JToken.FromObject(Variables.strings).ToString();"

{
  "singleValue": "",
  "allValues": {}
}
```

```json
"return JToken.FromObject(Variables.strings.AllValues).ToString();"

{}
```

```json
"return JToken.FromObject(Variables.strings.AllValues.Values).ToString();"

[]
```

```json
"return JToken.FromObject(Variables.strings.AllValues.Values.Select(x => x.SingleValue)).ToString();"

[]
```
"strings.Count().ToString();" ==> 0

### For nodes outputing items, with the text attribute populated

```json
"return JToken.FromObject(Variables.strings).ToString();"

{
  "singleValue": "abcdf, Hideous Pothole",
  "allValues": {
    "0": {
      "singleValue": "abcdf",
      "allValues": {
        "0": {
          "singleValue": "abcdf",
          "allValues": {}
        }
      }
    },
    "1": {
      "singleValue": "Hideous Pothole",
      "allValues": {
        "0": {
          "singleValue": "Hideous Pothole",
          "allValues": {}
        }
      }
    }
  }
}
```

```json
"return JToken.FromObject(Variables.strings.AllValues).ToString();"

{
  "0": {
    "singleValue": "abcdf",
    "allValues": {
      "0": {
        "singleValue": "abcdf",
        "allValues": {}
      }
    }
  },
  "1": {
    "singleValue": "Hideous Pothole",
    "allValues": {
      "0": {
        "singleValue": "Hideous Pothole",
        "allValues": {}
      }
    }
  }
}
```

```json
"return JToken.FromObject(Variables.strings.AllValues.Values).ToString();"

[
  {
    "singleValue": "abcdf",
    "allValues": {
      "0": {
        "singleValue": "abcdf",
        "allValues": {}
      }
    }
  },
  {
    "singleValue": "Hideous Pothole",
    "allValues": {
      "0": {
        "singleValue": "Hideous Pothole",
        "allValues": {}
      }
    }
  }
]
```

```json
"return JToken.FromObject(Variables.strings.AllValues.Values.Select(x => x.SingleValue)).ToString();"

[
  "abcdf",
  "Hideous Pothole"
]
```
### For nodes outputing items, without the string attribute populated

```json
"return JToken.FromObject(Variables.strings).ToString();"

{
  "singleValue": "",
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
"return JToken.FromObject(Variables.strings.AllValues).ToString();"

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
"return JToken.FromObject(Variables.strings.AllValues.Values).ToString();"

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
"return JToken.FromObject(Variables.strings.AllValues.Values.Select(x => x.SingleValue)).ToString();"

[
  null,
  null
]
```
