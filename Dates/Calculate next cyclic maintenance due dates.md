# Calculate next cyclic maintenance due dates

Some maintenance tasks must be carried out at regular intervals according to a pre-established frequency.

A clear example of that are street lighting inspection tasks such as:
- Lantern cleansing
- Lamp replacement
- Electrical tests
- Structural tests
- etc.

Normally in these cases, the completion of one of these tasks on a lighting unit is used to compute 
when the next task of the same type should be carried out on the same unit.

These calculations normally follow this pattern:

&nbsp;&nbsp;&nbsp;&nbsp;![nextDueDate = lastCompletionDate + cyclicFrequency](https://latex.codecogs.com/svg.latex?Next\hspace{1mm}due\hspace{1mm}date=Last\hspace{1mm}completion\hspace{1mm}date+Cyclic\hspace{1mm}frequency) 

<br/>

```json
{
    "parameters": [
        {
            "attributeCode": "attributes_streetLightsNextElectricalTest_6164124413abdf015b813c0c",
            "value": {
                "script": "return next_due_date;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        }
    ],
    "variables": [
        {
            "name": "last_completion_date",
            "value": {
                "inputParent": 0,
                "itemValue": {
                    "attributeCode": "attributes_streetLightsLastElectricalTestDate_5ebbffedf1168900487f4b61",
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeInputWebModel"
            }
        },
        {
            "name": "cyclic_frequency",
            "value": {
                "outputAction": "61978e9a347bd601574f292f",
                "itemValue": {
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel",
                    "attributeCode": "attributes_streetLightingUnitTypesElectricalTestCycle_617a74c728398b015948e08f"
                },
                "discriminator": "WorkflowSyntaxNodeOutputWebModel"
            }
        },
        {
            "name": "next_due_date",
            "value": {
                "script": "return last_completion_date.Value.AddMonths((int)cyclic_frequency.Value);",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        }
    ]
}
```
#### Explanation of C# objects, methods, etc.
- "last_completion_date" is a **DateTime?** C# object (nullable DateTime)
- "cyclic_frequency"  is a **Double?** C# object (nullable Double)
- Both are Alloy attributes stored either in the task design, the asset design or another related design 
- ".Value" converts **DateTime?** to **DateTime** and **Double?** to **Double**
- **DateTime**.AddMonths(Int) method adds months to a **DateTime** object"
  - The only argument required is the number of months to add as **Int**
  - Other useful **DateTime** methods can be found [here](https://docs.microsoft.com/en-us/dotnet/api/system.datetime?view=net-6.0)  e.g. .AddDays(), .AddMinutes(), etc.
- An explicit cast is required to convert from **Double** to **Int** -->"(int)cyclic_frequency.Value"
