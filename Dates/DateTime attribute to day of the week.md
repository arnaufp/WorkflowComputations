# DateTime attribute to day of the week

Given an Alloy DateTime attribute, get the day of the week and save it in a text attribute

<br/>


```json
{
    "parameters": [
        {
            "attributeCode": "attributes_defectsDescription",
            "value": {
                "script": "return reportedDateTime.Value.ToString(\"dddd\");",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        }
    ],
    "variables": [
        {
            "name": "reportedDateTime",
            "value": {
                "inputParent": 0,
                "itemValue": {
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel",
                    "attributeCode": "attributes_defectsReportedDate"
                },
                "discriminator": "WorkflowSyntaxNodeInputWebModel"
            }
        }
    ]
}
```
#### Explanation of C# objects, methods, etc.
- "reportedDateTime" is a **DateTime?** C# object (a nullable DateTime)
- If it has a value, we can get it with "reportedDateTime.Value" 
- ".ToString("dddd") converts the DateTime into a string. 
- "dddd" represents the full name of the day
- Other C# date and time formats can be found here ([standard](https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-date-and-time-format-strings) and [custom](https://docs.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings)) 
