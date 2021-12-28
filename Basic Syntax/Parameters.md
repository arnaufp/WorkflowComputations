# Parameters: Basic syntax

JSON snippets to copy & past and quickly start setting up a new computation

>### Constant (UI)
```json
{
    "attribute": {
        "attributeCode": "attributes_designMyNumberAttribute_5f06170ac3ca920067f1d829",
        "value": 42
    },
    "discriminator": "WorkflowConstantItemAttributeWebModel"
}
```

<br/>
<br/>

>### Computed
> - script
```json
{
    "attributeCode": "attributes_designMyAttribute_5f06170ac3ca920067f1d829",
    "value": {
        "script": "return taskPoints.Sum();",
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
    },
    "discriminator": "WorkflowComputedItemAttributeWebModel"
}
```
> - script with return option
```json
{
    "attributeCode": "attributes_projectsTasks",
    "value": {
        "script": "return tasks",
        "returnOptions": {
            "code": "designInterfaces_tasks",
            "graph": "Project",
            "discriminator": "DodiAttributeOptionsLinkWebModel"
        },
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
    },
    "discriminator": "WorkflowComputedItemAttributeWebModel"
}
```
> - template
```json
{
    "attributeCode": "attributes_workflowHttpRequestActionsBody",
    "value": {
        "template": "{\"case_id\":\"$caseId\", \"stage_name\":\"Action\", \"SLA_Date\":\"$remDate2\"}",
        "discriminator": "WorkflowSyntaxNodeTemplateWebModel"
    },
    "discriminator": "WorkflowComputedItemAttributeWebModel"
}
```
> - from input
```json
{
    "attributeCode": "attributes_designMyGeometryAttribute_5f06170ac3ca920067f1d829",
    "value": {
        "inputParent": 0,
        "itemValue": {
            "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel",
            "attributeCode": "attributes_itemsGeometry"
        },
        "discriminator": "WorkflowSyntaxNodeInputWebModel"
    },
    "discriminator": "WorkflowComputedItemAttributeWebModel"
}
```
> - from output
```json
{
    "attributeCode": "attributes_designMyGeometryAttribute_5f06170ac3ca920067f1d829",
    "value": {
        "outputAction": "5f05f85cc3ca920067f1d7a0",
        "itemValue": {
            "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel",
            "attributeCode": "attributes_itemsGeometry"
        },
        "discriminator": "WorkflowSyntaxNodeOutputWebModel"
    },
    "discriminator": "WorkflowComputedItemAttributeWebModel"
}
```
> - from offset
```json
{
    "attributeCode": "attributes_designMyDateTimeAttribute_5f06170ac3ca920067f1d829",
    "value": {
        "offsetMilliseconds": 86400000,
        "offsetOrigin": "Scheduled",
        "discriminator": "WorkflowSyntaxNodeRelativeTimeWebModel"
    },
    "discriminator": "WorkflowComputedItemAttributeWebModel"
}
```

<br/>
<br/>

>### Virtual definition
> - standard
```json
{
    "attributeCode": "attributes_designMyStringAttribute_5f06170ac3ca920067f1d829",
    "virtualDefinition": "$input(0)$attributes_name$ has £$input(1)$attributes_balance$",
    "discriminator": "WorkflowVirtualItemAttributeWebModel"
}
```
> - offset
```json
{
    "attributeCode": "attributes_finestPurchaseOrdersOrderDate",
    "virtualDefinition": "$utcnow(Both)$0$",
    "discriminator": "WorkflowVirtualItemAttributeWebModel"
}
```
