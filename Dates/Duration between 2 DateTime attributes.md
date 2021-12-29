# Duration between 2 DateTime attributes

Compute the duration between 2 Alloy DateTime attributes and save it as a decimal number attribute 

<br/>


```json
{
    "parameters": [
        {
            "attributeCode": "attributes_jobForTestingTotalHours_602d3b113cf282006c3fb0eb",
            "value": {
                "script": "return totalHours;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        },
        {
            "attributeCode": "attributes_jobForTestingTotalMinutes_602d3b1c39e0d6006a954155",
            "value": {
                "script": "return totalMinutes;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        },
        {
            "attributeCode": "attributes_jobForTestingTotalSeconds_602d3b2936db1900656fbe20",
            "value": {
                "script": "return totalSeconds;",
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
            "name": "completionDateTime",
            "value": {
                "inputParent": 0,
                "itemValue": {
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel",
                    "attributeCode": "attributes_tasksCompletionTime"
                },
                "discriminator": "WorkflowSyntaxNodeInputWebModel"
            }
        },
        {
            "name": "totalHours",
            "value": {
                "script": "var totalHours = (completionDateTime - startDateTime).Value.TotalHours; return totalHours;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "totalMinutes",
            "value": {
                "script": "var totalMinutes = (completionDateTime - startDateTime).Value.TotalMinutes; return totalMinutes;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "totalSeconds",
            "value": {
                "script": "var totalSeconds = (completionDateTime - startDateTime).Value.TotalSeconds; return totalSeconds;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        }
    ]
}
```
#### Explanation of C# objects, methods, etc. 
- "completionDateTime" and "startDateTime" are **DateTime?** C# objects (a nullable DateTime)
- Substracting 2 **DateTime?** objects (e.g. completionDateTime - startDateTime) returns a **TimeSpan?** C# object
- If **TimeSpan?** has a value, we can get it with ".Value" (**TimeSpan** C# object)
- The **TimeSpan** class and its properties and methods are described [here](https://docs.microsoft.com/en-us/dotnet/api/system.timespan?view=net-6.0)
- Some interesting properties:
  - **TimeSpan.TotalDays**, **TimeSpan.TotalHours**, **TimeSpan.TotalMinutes**, **TimeSpan.TotalSeconds** return the TimeSpan value expressed in whole and fractional days/hours/minutes/seconds (**Double**)
  - **TimeSpan.Days**, **TimeSpan.Hours**, **TimeSpan.Minutes**, **TimeSpan.Seconds** return the TimeSpan value expressed in whole days/hours/minutes/seconds (**Int32**)
