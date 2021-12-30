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
            "name": "bankHolidays",
            "value": {
                "outputAction": "60acfc7c5bfa7a0231013247",
                "itemValue": {
                    "attributeCode": "attributes_holidaysStartDate",
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeOutputWebModel"
            }
        },
        {
            "name": "workingDays",
            "value": {
                "outputAction": "6110f227211c79025193e4ad",
                "itemValue": {
                    "attributeCode": "attributes_taskPrioritiesWorkingDays_610bf49a211c7902519149f3",
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
                "script": "DateTime new_job_target_time = new DateTime(); var movedRaisedTime = job_raised_time.Value; var daysToCheck = Enumerable.Range(1, 365); var validWorkingDays = daysToCheck.Where(n=>n==1).Select(d=>new DateTime()); if(movedRaisedTime.DayOfWeek == DayOfWeek.Saturday){movedRaisedTime = movedRaisedTime.Date.AddDays(2).AddHours(businessStartHourUTC.Value);} else if(movedRaisedTime.DayOfWeek == DayOfWeek.Sunday){movedRaisedTime = movedRaisedTime.Date.AddDays(1).AddHours(businessStartHourUTC.Value);}else if(movedRaisedTime>movedRaisedTime.Date.AddHours(businessEndHourUTC.Value) && movedRaisedTime.DayOfWeek== DayOfWeek.Friday){movedRaisedTime = movedRaisedTime.Date.AddDays(3).AddHours(businessStartHourUTC.Value);} else if(movedRaisedTime>movedRaisedTime.Date.AddHours(businessEndHourUTC.Value)){movedRaisedTime = movedRaisedTime.Date.AddDays(1).AddHours(businessStartHourUTC.Value);} else if(movedRaisedTime < movedRaisedTime.Date.AddHours(businessStartHourUTC.Value)){movedRaisedTime = movedRaisedTime.Date.AddHours(businessStartHourUTC.Value);} if (movedRaisedTime==movedRaisedTime.Date.AddHours(businessStartHourUTC.Value)){validWorkingDays = daysToCheck.Where(d=>movedRaisedTime.Date.AddDays(d-1).AddHours(businessEndHourUTC.Value).DayOfWeek !=DayOfWeek.Saturday && movedRaisedTime.Date.AddDays(d-1).AddHours(businessEndHourUTC.Value).DayOfWeek !=DayOfWeek.Sunday && !Variables.bankHolidays.AllValues.Values.Select(x => x.SingleValue).Contains(Date(movedRaisedTime.Date.AddDays(d-1).AddHours(businessEndHourUTC.Value)))).Select(d => movedRaisedTime.Date.AddDays(d-1).AddHours(businessEndHourUTC.Value));} else{validWorkingDays = daysToCheck.Where(d=>movedRaisedTime.AddDays(d).DayOfWeek !=DayOfWeek.Saturday && movedRaisedTime.AddDays(d).DayOfWeek !=DayOfWeek.Sunday && !Variables.bankHolidays.AllValues.Values.Select(x => x.SingleValue).Contains( Date(movedRaisedTime.AddDays(d)))).Select(d => movedRaisedTime.AddDays(d));}; new_job_target_time = validWorkingDays.ElementAt((int)priority_quantity_of_time.Value-1); return new_job_target_time;",
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
// init variable that will store the offseted target time
DateTime new_job_target_time = new DateTime();

// variable used to move (forward) the Raised Time
var movedRaisedTime = job_raised_time.Value;

/* Loops are not allowed in WFC. 
To overcome this it uses the Enumerable C# class (System.Linq.Enumerable) and its LINQ methods
Here it creates an Enumerable that holds all values from 1 to 365. */
var daysToCheck = Enumerable.Range(1, 365); 

// init Enumerable that only holds one DateTime
var validWorkingDays = daysToCheck.Where(n => n == 1).Select(d => new DateTime()); 

// If Raised Time is a Saturday moves it to next Monday at 8h
if(movedRaisedTime.DayOfWeek == DayOfWeek.Saturday){
    movedRaisedTime = movedRaisedTime.Date.AddDays(2).AddHours(businessStartHourUTC.Value);
}

// Else if Raised Time is a Sunday moves it to next Monday at 8h
else if(movedRaisedTime.DayOfWeek == DayOfWeek.Sunday){
    movedRaisedTime = movedRaisedTime.Date.AddDays(1).AddHours(businessStartHourUTC.Value);
}

// Else if Raised Time is a Friday after 17h moves it to next Monday at 8h
else if(movedRaisedTime > movedRaisedTime.Date.AddHours(businessEndHourUTC.Value) && movedRaisedTime.DayOfWeek == DayOfWeek.Friday){
    movedRaisedTime = movedRaisedTime.Date.AddDays(3).AddHours(businessStartHourUTC.Value);
} 

//  Else if Raised Time is after 17h moves it to next day at 8h
else if(movedRaisedTime > movedRaisedTime.Date.AddHours(businessEndHourUTC.Value)){
    movedRaisedTime = movedRaisedTime.Date.AddDays(1).AddHours(businessStartHourUTC.Value);
} 

// Else if Raised Time is before 8h moves it to the same day at 8h
else if(movedRaisedTime < movedRaisedTime.Date.AddHours(businessStartHourUTC.Value)){
    movedRaisedTime = movedRaisedTime.Date.AddHours(businessStartHourUTC.Value);
} 


// At this point the Raised Time has been moved to a valid working hour

/* 
IF the Raised Time is at 8h
use Enumerable LINQ methods to "loop/iterate" from 1 to 365
for each number (d), add "d" days to the Raised Time e.g. Raised Time +1day, +2days, +days, etc.
if the resulting day is neither a Saturday nor Sunday nor a Bank Holiday then add that day (at 17h) to the "validWorkingDays" Enumerable
*/
if (movedRaisedTime == movedRaisedTime.Date.AddHours(businessStartHourUTC.Value)){
    validWorkingDays = daysToCheck.Where(d => 
        movedRaisedTime.Date.AddDays(d-1).AddHours(businessEndHourUTC.Value).DayOfWeek != DayOfWeek.Saturday && 
        movedRaisedTime.Date.AddDays(d-1).AddHours(businessEndHourUTC.Value).DayOfWeek != DayOfWeek.Sunday &&
        !Variables.bankHolidays.AllValues.Values.Select(x => x.SingleValue)
            .Contains(Date(movedRaisedTime.Date.AddDays(d-1).AddHours(businessEndHourUTC.Value)))
    ) 
    .Select(d => 
        movedRaisedTime.Date.AddDays(d - 1).AddHours(businessEndHourUTC.Value)
    );
}

/*
ELSE the Raised time is not at 8h, it must be between 8h and 17h
As before "loop/iterate" from 1 to 365
for each number (d), add "d" days to the Raised Time e.g. Raised Time +1day, +2days, +days, etc.
if the resulting day is neither a Saturday nor a Sunday nor a Bank Holiday then add that day (and time) to the "validWorkingDays" Enumerable
*/
else{
    validWorkingDays = daysToCheck.Where(d => 
        movedRaisedTime.AddDays(d).DayOfWeek !=DayOfWeek.Saturday && 
        movedRaisedTime.AddDays(d).DayOfWeek !=DayOfWeek.Sunday &&
        !Variables.bankHolidays.AllValues.Values.Select(x => x.SingleValue)
            .Contains(Date(movedRaisedTime.AddDays(d)))
    )
    .Select(d => 
        movedRaisedTime.AddDays(d)
    );
} 

/*
At this point the "validWorkingDays" Enumerable holds a list of valid DateTime objects e.g. Raised Time +1 working day, +2 working days, etc.
To get the offset target time, it uses .ElementAt to return the element at a specified index (number of working days) of the enumerable
*/
new_job_target_time = validWorkingDays.ElementAt((int)workingDays.Value-1);

return new_job_target_time;
```
#### Explanation of C# objects, methods, etc.
- "Date(**DateTime**)" converts a **DateTime** to **AlloyEngine.DataModels.Date** C# object
- "Time(**DateTime**)" converts a **DateTime** to **AlloyEngine.DataModels.Time** C# object
- Date Alloy attributes expect to receive **AlloyEngine.DataModels.Date**
- Time Alloy attributes expect to receive **AlloyEngine.DataModels.Time**
