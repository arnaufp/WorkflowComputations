# Target Time = Raised Time + Working Days Offset

Various customers requested the ability to automatically compute and set the Target Time of a task by offsetting a certain amount of time to the Raised Time.
This can be done in the UI with the offset functionality when configuring DateTime attributes in a workflow node.
However, currently the Offset in the UI doesn't take into account working days/hours.

To overcome this limitation a workflow computation can be configured. This must take into account the concept of working days/hours:
- Only weekdays: Monday to Friday
- Only business hours: e.g. 8h to 17h
- Public Holidays must be taken into consideration



<br/>


```json
{
    "parameters": [
        {
            "attributeCode": "attributes_tasksTargetTime",
            "value": {
                "script": "return new_job_target_time;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        }
    ],
    "variables": [
        {
            "name": "job_raised_time",
            "value": {
                "inputParent": 0,
                "itemValue": {
                    "attributeCode": "attributes_tasksRaisedTime",
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeInputWebModel"
            }
        },
        {
            "name": "priority_quantity_of_time",
            "value": {
                "outputAction": "6110f227211c79025193e4ad",
                "itemValue": {
                    "attributeCode": "attributes_taskPrioritiesQuantityOfTime_610bf49a211c7902519149f3",
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeOutputWebModel"
            }
        },
        {
            "name": "priority_period",
            "value": {
                "outputAction": "6110f239f7d34802554f7c8e",
                "itemValue": {
                    "attributeCode": "attributes_taskPriorityPeriodsPriorityPeriod_610bed9d211c790251913d92",
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeOutputWebModel"
            }
        },
        {
            "name": "businessStartHour",
            "value": {
                "script": "return 8;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "businessStartHourUTC",
            "value": {
                "script": "var nowUTC= Now;var nowLocal=Local(nowUTC);var ts = nowLocal-nowUTC;var utcOffset=ts.Value.Hours; return businessStartHour - utcOffset;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "businessEndHour",
            "value": {
                "script": "return 17;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "businessEndHourUTC",
            "value": {
                "script": "var nowUTC= Now;var nowLocal=Local(nowUTC);var ts = nowLocal-nowUTC;var utcOffset=ts.Value.Hours; return businessEndHour - utcOffset;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "new_job_target_time",
            "value": {
                "script": "DateTime new_job_target_time = new DateTime(); if(priority_period==\"Hours\"){new_job_target_time=job_raised_time.Value.AddHours(priority_quantity_of_time.Value);}; if(priority_period==\"Days\"){new_job_target_time=job_raised_time.Value.AddDays(priority_quantity_of_time.Value);}; var daysToAdd=1; if(priority_period==\"End of Next Working Day\"){if(job_raised_time.Value.DayOfWeek==DayOfWeek.Friday){daysToAdd=3;}else if(job_raised_time.Value.DayOfWeek==DayOfWeek.Saturday){daysToAdd=2;}; new_job_target_time=job_raised_time.Value.Date.AddDays(daysToAdd).AddHours(businessEndHourUTC.Value);}; var movedRaisedTime = job_raised_time.Value; var daysToCheck = Enumerable.Range(1, 365); var validWorkingDays = daysToCheck.Where(n=>n==1).Select(d=>new DateTime()); if(priority_period==\"Working Days\"){if(movedRaisedTime.DayOfWeek == DayOfWeek.Saturday){movedRaisedTime = movedRaisedTime.Date.AddDays(2).AddHours(businessStartHourUTC.Value);} else if(movedRaisedTime.DayOfWeek == DayOfWeek.Sunday){movedRaisedTime = movedRaisedTime.Date.AddDays(1).AddHours(businessStartHourUTC.Value);}else if(movedRaisedTime>movedRaisedTime.Date.AddHours(businessEndHourUTC.Value) && movedRaisedTime.DayOfWeek== DayOfWeek.Friday){movedRaisedTime = movedRaisedTime.Date.AddDays(3).AddHours(businessStartHourUTC.Value);} else if(movedRaisedTime>movedRaisedTime.Date.AddHours(businessEndHourUTC.Value)){movedRaisedTime = movedRaisedTime.Date.AddDays(1).AddHours(businessStartHourUTC.Value);} else if(movedRaisedTime < movedRaisedTime.Date.AddHours(businessStartHourUTC.Value)){movedRaisedTime = movedRaisedTime.Date.AddHours(businessStartHourUTC.Value);} if (movedRaisedTime==movedRaisedTime.Date.AddHours(businessStartHourUTC.Value)){validWorkingDays = daysToCheck.Where(d=>movedRaisedTime.Date.AddDays(d-1).AddHours(businessEndHourUTC.Value).DayOfWeek !=DayOfWeek.Saturday && movedRaisedTime.Date.AddDays(d-1).AddHours(businessEndHourUTC.Value).DayOfWeek !=DayOfWeek.Sunday).Select(d=>movedRaisedTime.Date.AddDays(d-1).AddHours(businessEndHourUTC.Value));} else{validWorkingDays = daysToCheck.Where(d=>movedRaisedTime.AddDays(d).DayOfWeek !=DayOfWeek.Saturday && movedRaisedTime.AddDays(d).DayOfWeek !=DayOfWeek.Sunday).Select(d=>movedRaisedTime.AddDays(d));}; new_job_target_time = validWorkingDays.ElementAt((int)priority_quantity_of_time.Value-1);}; return new_job_target_time;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        }
    ]
}
```
```csharp
var movedRaisedTime = job_raised_time.Value;
var daysToCheck = Enumerable.Range(1, 365);
```
```csharp
var movedRaisedTime = job_raised_time.Value; 
var daysToCheck = Enumerable.Range(1, 365); 
var validWorkingDays = daysToCheck.Where(n=>n==1).Select(d=>new DateTime()); 

if(movedRaisedTime.DayOfWeek == DayOfWeek.Saturday){
    movedRaisedTime = movedRaisedTime.Date.AddDays(2).AddHours(businessStartHourUTC.Value);
} 
else if(movedRaisedTime.DayOfWeek == DayOfWeek.Sunday){
    movedRaisedTime = movedRaisedTime.Date.AddDays(1).AddHours(businessStartHourUTC.Value);
}
else if(movedRaisedTime>movedRaisedTime.Date.AddHours(businessEndHourUTC.Value) && movedRaisedTime.DayOfWeek== DayOfWeek.Friday){
    movedRaisedTime = movedRaisedTime.Date.AddDays(3).AddHours(businessStartHourUTC.Value);
} 
else if(movedRaisedTime>movedRaisedTime.Date.AddHours(businessEndHourUTC.Value)){
    movedRaisedTime = movedRaisedTime.Date.AddDays(1).AddHours(businessStartHourUTC.Value);
} 
else if(movedRaisedTime < movedRaisedTime.Date.AddHours(businessStartHourUTC.Value)){
    movedRaisedTime = movedRaisedTime.Date.AddHours(businessStartHourUTC.Value);
} 

if (movedRaisedTime==movedRaisedTime.Date.AddHours(businessStartHourUTC.Value)){
    validWorkingDays = daysToCheck.Where(d=>movedRaisedTime.Date.AddDays(d-1).AddHours(businessEndHourUTC.Value).DayOfWeek !=DayOfWeek.Saturday && 
    movedRaisedTime.Date.AddDays(d-1).AddHours(businessEndHourUTC.Value).DayOfWeek !=DayOfWeek.Sunday).Select(d=>movedRaisedTime.Date.AddDays(d-
    1).AddHours(businessEndHourUTC.Value));
} 
else{
    validWorkingDays = daysToCheck.Where(d=>movedRaisedTime.AddDays(d).DayOfWeek !=DayOfWeek.Saturday && movedRaisedTime.AddDays(d).DayOfWeek 
    !=DayOfWeek.Sunday).Select(d=>movedRaisedTime.AddDays(d));
} 

new_job_target_time = validWorkingDays.ElementAt((int)priority_quantity_of_time.Value-1);
 

return new_job_target_time;

```
#### Explanation of C# objects, methods, etc.
- "Date(**DateTime**)" converts a **DateTime** to **AlloyEngine.DataModels.Date** C# object
- "Time(**DateTime**)" converts a **DateTime** to **AlloyEngine.DataModels.Time** C# object
- Date Alloy attributes expect to receive **AlloyEngine.DataModels.Date**
- Time Alloy attributes expect to receive **AlloyEngine.DataModels.Time**
