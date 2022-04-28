# Variables: Basic syntax

JSON snippets to copy & past and quickly start setting up a new computation

>### Script
```json
{
    "name": "myVariable",
    "value": {
        "script": "var rnd = new Random();return rnd.Next(100,200);",
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
    }
}
```

<br/>
<br/>

>### Input
> - attribute

```json
{
    "name": "myVariable",
    "value": {
        "inputParent": 0,
        "itemValue": {
            "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel",
            "attributeCode": "attributes_itemsGeometry"
        },
        "discriminator": "WorkflowSyntaxNodeInputWebModel"
    }
}
```
> - property
```json
{
    "name": "myVariable",
    "value": {
        "inputParent": 0,
        "itemValue": {
            "discriminator": "WorkflowSyntaxArgumentItemValueItemPropertyWebModel",
            "property": "ItemId"
        },
        "discriminator": "WorkflowSyntaxNodeInputWebModel"
    }
}
```
> - variable
```json
{
  "name": "myVariable",
  "value": {
    "inputParent": 1,
    "itemValue": {
      "discriminator": "WorkflowSyntaxArgumentItemValueVariableWebModel",
      "variableName": "variableOnPrecedingNode"
    },
    "discriminator": "WorkflowSyntaxNodeInputWebModel"
  }
}
```
<br/>
<br/>

>### Output
> - attribute

```json
{
    "name": "myVariable",
    "value": {
        "outputAction": "5f05f85cc3ca920067f1d7a0",
        "itemValue": {
            "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel",
            "attributeCode": "attributes_itemsGeometry"
        },
        "discriminator": "WorkflowSyntaxNodeOutputWebModel"
    }
}
```
> - property
```json
{
    "name": "myVariable",
    "value": {
        "outputAction": "5f05f85cc3ca920067f1d7a0",
        "itemValue": {
            "discriminator": "WorkflowSyntaxArgumentItemValueItemPropertyWebModel",
            "property": "ItemId"
        },
        "discriminator": "WorkflowSyntaxNodeOutputWebModel"
    }
}
```
> - variable
```json
{
  "name": "myVariable",
  "value": {
    "outputAction": "5f05f85cc3ca920067f1d7a0",
    "itemValue": {
      "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel",
      "attributeCode": "attributes_itemsGeometry"
    },
    "discriminator": "WorkflowSyntaxNodeOutputWebModel"
  }
}
```
<br/>
<br/>

>### Offset
> - started (the time the workflow run started)

```json
{
    "name": "timeStarted",
    "value": {
        "offsetMilliseconds": 0,
        "offsetOrigin": "Started",
        "discriminator": "WorkflowSyntaxNodeRelativeTimeWebModel"
    }
}
```
> - triggered (the time the workflow triggered)
```json
{
    "name": "timeTriggered",
    "value": {
        "offsetMilliseconds": 0,
        "offsetOrigin": "Triggered",
        "discriminator": "WorkflowSyntaxNodeRelativeTimeWebModel"
    }
}
```
> - scheduled (the time the workflow was scheduled to trigger)
```json
{
  "name": "timeScheduled",
  "value": {
    "offsetMilliseconds": 0,
    "offsetOrigin": "Scheduled",
    "discriminator": "WorkflowSyntaxNodeRelativeTimeWebModel"
  }
}
```

<br/>
<br/>

>### AQS
```json
{
    "name": "allStreetLights",
    "value": {
        "aqs": {
            "type": "Query",
            "properties": {
                "dodiCode": "designs_streetLights",
                "collectionCode": [
                    "Live"
                ],
                "attributes": []
            }
        },
        "discriminator": "WorkflowSyntaxNodeAqsWebModel"
    }
}
```

<br/>
<br/>

>### Template
```json
{
    "name": "myStringVariable",
    "value": {
        "template": "$myNameVariable has £$myMoneyVariable",
        "discriminator": "WorkflowSyntaxNodeTemplateWebModel"
    }
}
```
