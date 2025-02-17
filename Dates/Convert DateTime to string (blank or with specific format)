# Convert DateTime to string (blank or with specific format)

DateTimes attributes can be converted into string with .ToString() C# method. This method has a parameter to define which format you want the string to be.
Complete list of format specifiers and their definitions can be found [here](https://learn.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings)

```json
{
    "variables": [
        {
      "name": "remediedDate0",
      "value": {
        "inputParent": 0,
        "itemValue": {
          "attributeCode": "attributes_defectsRemediedDate",
          "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
        },
        "discriminator": "WorkflowSyntaxNodeInputWebModel"
      }
    },
    {
      "name": "remediedDate",
      "value": {
        "script": "var remediedDate =\"\"; if(remediedDate0 != null){remediedDate = remediedDate0.Value.ToString(\"yyyy-MM-ddTHH:mm:ss.000Z\");}; return remediedDate;",
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
      }
    }
    ]
}
```
#### Explanation of C# objects, methods, etc.
- "remediedDate0" is a **DateTime?** C# object (nullable DateTime)
- ".Value" converts **DateTime?** to **DateTime** 
- **DateTime**.ToString() string formats the datetime using the format specifiers passed as argument.
