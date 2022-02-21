# Link multiple items from any workflow nodes to an email


Configuring an Email Message node through the Alloy UI allows you 3 options to select and attach Linked Items to the email:
1. **Constant Tab**: manually select multiple Alloy items. Attached items will always be the same no matter the items used within each workflow run.
2. **Link Tab**: select Alloy items outputted from a previous workflow node. It is a dynamic setting, thus the item/s will depend on each different workflow run. 
3. **Output Tab**: select Alloy items outputted from any workflow node (it doesn't need to be in the same commit chain/branch). It is a dynamic setting, thus the item/s will depend on each different workflow run.

<br/>

**Options 2 and 3 only allows you to select one single node as target, but there might be scenarios where you want to attach items from different nodes to the email.**

<br/>

**Example**

A workflow that triggers on creation of Defects and checks whether the Defect is a duplicate, hence another Defect already exists and a Job has already been raised.
You may want to issue an email to a user to notify that there is a duplicate Defect and attach both the original Defect, the original Raised Job and the duplicate Defect.

<br/>

### Solution
This can be achieved by creating as many variables (input or output) within the Email Message node as Linked Items you want to attach.
Then you need to concatenate them all and pass them as **attributes_workflowMessageActionLinkedItems** parameter/attribute.

<br/>

```json
{
    "actionDesignCode": "designs_workflowMessageAction",
    "parameters": [
        {
            "attribute": {
                "attributeCode": "attributes_workflowMessageActionMessageType",
                "value": [
                    "5c66bcd44b4d4259071069de" 
                ]
            },
            "discriminator": "WorkflowConstantItemAttributeWebModel"
        },
        {
            "attributeCode": "attributes_workflowMessageActionMessageText",
            "value": {
                "template": "DUPLICATE DEFECT SUBMITTED. Defect \"$current_defect_title\" is a duplicate of Defect \"$original_defect_title\", from which Job \"$original_job_title\" was raised",
                "discriminator": "WorkflowSyntaxNodeTemplateWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        },
        {
            "attribute": {
                "attributeCode": "attributes_workflowMessageActionRecipientName",
                "value": " there"
            },
            "discriminator": "WorkflowConstantItemAttributeWebModel"
        },
        {
            "attributeCode": "attributes_workflowMessageActionLinkedItems",
            "value": {
                "script": "return linked_items;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        },
        {
            "attribute": {
                "attributeCode": "attributes_workflowMessageActionEmailAddress",
                "value": "user@email.com"
            },
            "discriminator": "WorkflowConstantItemAttributeWebModel"
        }
    ],
    "variables": [
        {
            "name": "original_defect",
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
            "name": "original_job",
            "value": {
                "inputParent": 2,
                "itemValue": {
                    "property": "ItemId",
                    "discriminator": "WorkflowSyntaxArgumentItemValueItemPropertyWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeInputWebModel"
            }
        },
        {
            "name": "current_defect",
            "value": {
                "inputParent": 3,
                "itemValue": {
                    "property": "ItemId",
                    "discriminator": "WorkflowSyntaxArgumentItemValueItemPropertyWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeInputWebModel"
            }
        },
        {
            "name": "linked_items",
            "value": {
                "script": "return current_defect.Concat(original_defect).Concat(original_job);",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "original_defect_title",
            "value": {
                "inputParent": 0,
                "itemValue": {
                    "attributeCode": "attributes_itemsTitle",
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeInputWebModel"
            }
        },
        {
            "name": "original_job_title",
            "value": {
                "inputParent": 2,
                "itemValue": {
                    "attributeCode": "attributes_itemsTitle",
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeInputWebModel"
            }
        },
        {
            "name": "current_defect_title",
            "value": {
                "inputParent": 3,
                "itemValue": {
                    "attributeCode": "attributes_itemsTitle",
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeInputWebModel"
            }
        }
    ]
}
```

<br/>

\* Potentially, another possible (but untested) option could be to set up a specific Query Node that queries the Items interface (designInterfaces_items) and returns all the items you want. 
Though, probably you will also need some kind of WFC to configure the Query parameter/s dynamically.


