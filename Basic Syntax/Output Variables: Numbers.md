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

```json
"return JToken.FromObject(Variables.numbers).ToString();"

{
  "allValues": {}
}
```

```json
"return JToken.FromObject(Variables.numbers.AllValues).ToString();"

{}
```

```json
"return JToken.FromObject(Variables.numbers.AllValues.Values).ToString();"

[]
```
"Variables.numbers.AllValues.Values.Sum(x => x.SingleValue);" ==> 0

### For nodes outputing items, with the number attribute populated

```json
"return JToken.FromObject(Variables.numbers).ToString();"

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

```json
"return JToken.FromObject(Variables.numbers.AllValues).ToString();"

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

```json
"return JToken.FromObject(Variables.numbers.AllValues.Values).ToString();"

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

### For nodes outputing items, without the number attribute populated

```json
"return JToken.FromObject(Variables.numbers).ToString();"

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
"return JToken.FromObject(Variables.numbers.AllValues).ToString();"

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
"return JToken.FromObject(Variables.numbers.AllValues.Values).ToString();"

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
"Variables.numbers.AllValues.Values.Sum(x => x.SingleValue);" ==> 0
