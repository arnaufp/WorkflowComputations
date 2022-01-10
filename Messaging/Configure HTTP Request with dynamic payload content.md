# Configure HTTP Request with dynamic payload content

Within Allow Web HTTP Requests (Webhooks) can be set as action nodes of workflows. There are 4 parameters that need to be configured by users:
- HTTP method / verb (get, post, put, etc.)
- HTTP headers
- Webhook endpoint URL
- Webhook body / payload

<br/>

Though configuring an HTTP request node in th UI is possible, doing it through the API and computations provides a much more flexible solution. 
Primarly, using computations provides the ability to fully configure the desired structure of the request bodies or payloads.

<br/>

The following example adds an HTTP Request node to a workflow. 
When this node is reached by a workflow run, it will dynamically create a payload using the specified template and send this request:

```
POST / HTTP/1.1
Host: blackburndemo.requestcatcher.com
Content-Type: application/json
Content-Length: 209

{
    "alloyItemId": "<<Alloy item id (job)>>",
    "jobNumber": "<<Alloy job number>>",
    "completionTime": "<<yyyy-MM-ddTHH:mm:ssZ>>",
    "taskStatus": "<<status>>",
    "assetAlloyId": "<<Alloy item id (asset)>>"
}

```

```json
{
    "actionDesignCode": "designs_workflowHttpRequestAction",
    "parameters": [
        {
            "attribute": {
                "attributeCode": "attributes_workflowHttpRequestActionsHttpMethod",
                "value": [
                    "5c6bd2fc4b4d4259071069e1"
                ]
            },
            "discriminator": "WorkflowConstantItemAttributeWebModel"
        },
        {
            "attribute": {
                "attributeCode": "attributes_workflowHttpRequestActionsHttpHeaders",
                "value": "Content-Type: application/json"
            },
            "discriminator": "WorkflowConstantItemAttributeWebModel"
        },
        {
            "attribute": {
                "attributeCode": "attributes_workflowHttpRequestActionsUrl",
                "value": "https://blackburndemo.requestcatcher.com/"
            },
            "discriminator": "WorkflowConstantItemAttributeWebModel"
        },
        {
            "attributeCode": "attributes_workflowHttpRequestActionsBody",
            "value": {
                "template": "{\"alloyItemId\": \"$alloyItemId\", \"jobNumber\": \"$jobNumber\",\"completionTime\": \"$completionTime2\",\"taskStatus\":\"$taskStatus\",\"assetAlloyId\":\"$assetAlloyId\"}",
                "discriminator": "WorkflowSyntaxNodeTemplateWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        }
    ],
    "variables": [
        {
            "name": "alloyItemIdArray",
            "value": {
                "inputParent": 0,
                "itemValue": {
                    "property": "ItemId",
                    "discriminator": "WorkflowSyntaxArgumentItemValueItemPropertyWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeInputWebModel"
            }
        },
        {
            "name": "alloyItemId",
            "value": {
                "script": "return alloyItemIdArray[0];",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "jobNumber",
            "value": {
                "inputParent": 0,
                "itemValue": {
                    "attributeCode": "attributes_jobsJobNumber",
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeInputWebModel"
            }
        },
        {
            "name": "completionTime1",
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
            "name": "completionTime2",
            "value": {
                "script": "string completionTime2=\"\";if(completionTime1!=null){completionTime2=completionTime1.Value.ToString(\"yyyy-MM-ddTHH:mm:ssZ\");};return completionTime2;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "taskStatus",
            "value": {
                "outputAction": "60e711fb6ad086024dc5cab3",
                "itemValue": {
                    "attributeCode": "attributes_taskStatusesStatus",
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeOutputWebModel"
            }
        },
        {
            "name": "assetAlloyIdArray",
            "value": {
                "outputAction": "60e712291a393a02558bbd8c",
                "itemValue": {
                    "property": "ItemId",
                    "discriminator": "WorkflowSyntaxArgumentItemValueItemPropertyWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeOutputWebModel"
            }
        },
        {
            "name": "assetAlloyId",
            "value": {
                "script": "return assetAlloyIdArray[0];",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        }
    ]
}
```

### Available HTTP methods and Alloy IDs
| Method | ID |
|----------|:-------------:|
| GET | 5c6bd2fc4b4d4259071069df |
| PUT | 5c6bd2fc4b4d4259071069e0 |
| POST | 5c6bd2fc4b4d4259071069e1 |
| DELETE | 5c6bd2fc4b4d4259071069e2 |
| HEAD | 5c6bd2fc4b4d4259071069e3 |
| OPTIONS | 5c6bd2fc4b4d4259071069e4 |
| TRACE | 5c6bd2fc4b4d4259071069e5 |

### Requirements
- Relation Node from the Job to the Status
- Relation node from the Job to the Asset

#### Explanation of C# objects, methods, etc. 
- Both "alloyItemIdArray" and "assetAlloyIdArray" variables are arrays of Alloy item ids
- "alloyItemIdArray[0]" and "assetAlloyIdArray[0]" return the first id stored in the array
- "completionTime1" is a **DateTime?** C# object (a nullable DateTime)
- If it has a value, we can get it with "completionTime1.Value" (C# **DateTime** object)
- DateTime.ToString(String) converts the value of the **DateTime** object to its equivalent string representation using the specified format
  - e.g. DateTime.ToString("yyyy-MM-ddTHH:mm:ssZ") ==> "2022-01-10T14:30:00Z"
