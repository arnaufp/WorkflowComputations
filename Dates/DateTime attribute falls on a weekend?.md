# DateTime attribute falls on a weekend?

Given an Alloy DateTime attribute determine whether it falls on a weekend or it is a weekday.

<br/>


```json
{
    "parameters": [
        {
            "attributeCode": "attributes_jobTestDayType_602d410e39e0d6006a9546f1",
            "value": {
                "script": "return dayType;",
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
            "name": "dayType",
            "value": {
                "script": "var dayType= \"weekday\"; var day = startDateTime.Value.DayOfWeek;if((day == DayOfWeek.Saturday) || (day == DayOfWeek.Sunday)){dayType=\"weekend\";} return dayType;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        }
    ]
}
```
#### Explanation of C# objects, methods, etc. 
- "startDateTime" is a **DateTime?** C# object (a nullable DateTime)
- If it has a value, we can get it with "startDateTime.Value" (**DateTime** C# object)
- "startDateTime.Value.DayOfWeek" returns a **DayOfWeek** enum C# object
- "day = DayOfWeek.Saturday" or "day = DayOfWeek.Sunday" checks whether the date falls on a weekend
