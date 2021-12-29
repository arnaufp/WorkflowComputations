# DateTime attribute to Date and Time attributes

Given an Alloy DateTime attribute convert it and store it as Date and Time attributes

<br/>


```json
{
    "parameters": [
        {
            "attributeCode": "attributes_jobTestStartDate_602d410e39e0d6006a9546f1",
            "value": {
                "script": "return startDate;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        },
        {
            "attributeCode": "attributes_jobTestStartTime_602e303b56a33800665c406e",
            "value": {
                "script": "return startTime;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        }
    ],
    "variables": [
        {
            "name": "startDateTime",
            "value": {
                "inputParent": 0,
                "itemValue": {
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel",
                    "attributeCode": "attributes_tasksStartTime"
                },
                "discriminator": "WorkflowSyntaxNodeInputWebModel"
            }
        },
        {
            "name": "startDate",
            "value": {
                "script": "var startDate = Date(startDateTime); return startDate;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "startTime",
            "value": {
                "script": "var startTime = Time(startDateTime); return startTime;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        }
    ]
}
```
#### Explanation of C# objects, methods, etc. s
- "Date(**DateTime**)" converts a **DateTime** to **AlloyEngine.DataModels.Date** C# object
- "Time(**DateTime**)" converts a **DateTime** to **AlloyEngine.DataModels.Time** C# object
- Date Alloy attributes expect to receive **AlloyEngine.DataModels.Date**
- Time Alloy attributes expect to receive **AlloyEngine.DataModels.Time**
