# Convert DateTime to string (with specific format)

DateTimes attributes can be converted into string with .ToString() C# method. This method has a parameter to define which format you want the string to be.
Complete list of format specifiers and their definitions can be found [here](https://learn.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings)

```json
{
    "variables": [
        {
      "name": "targetTime",
      "value": {
        "inputParent": 0,
        "itemValue": {
          "attributeCode": "attributes_tasksTargetTime",
          "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
        },
        "discriminator": "WorkflowSyntaxNodeInputWebModel"
      }
    },
        {
      "name": "targetTimeString",
      "value": {
        "script": "return targetTime.Value.AddDays(-1).ToString(\"dd/MM/yyyy\") + \" 09:05\";",
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
      }
    }
    ]
}
```
#### Explanation of C# objects, methods, etc.
- "targetTime" is a **DateTime?** C# object (nullable DateTime)
- ".Value" converts **DateTime?** to **DateTime** 
- **DateTime**.ToString() string formats the datetime using the format specifiers passed as argument.
