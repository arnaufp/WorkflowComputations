# Issue emails to multiple recipients

### Customer request (BWC): 

Send email notifications to multiple email addresses (recipients)

### Solution
This can be achieved by configuring as many Message nodes as email addresses (recipients) we want to send email to.\
A cleaner and more reusable approach is to store all the email addresses in a design. By doing this it will be much more easy to add or remove emails in the future.

This requires minimum 1 design and 2 Workflow Nodes:
1. A design with a text attribute to store all the emails e.g.:
    - "Email List" design (designs_dWMCEmails_61a9efba6809f1015548aa86)
    - with an "Email" text attribute (attributes_dWMCEmailsEmail_61a9efc007907b015bb6675e)
3. A Query node to get all the items of the "Email List" design
4. A computed Message Node connected to the Query Node 

<p align="center">
  <img src="query%2Bemail.png" alt="Query + Message Nodes"/> 
</p>

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
                "template": "This is an email notification example!",
                "discriminator": "WorkflowSyntaxNodeTemplateWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        },
        {
            "attributeCode": "attributes_workflowMessageActionRecipientName",
            "value": {
                "template": "there",
                "discriminator": "WorkflowSyntaxNodeTemplateWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        },
        {
            "attributeCode": "attributes_workflowMessageActionEmailAddress",
            "virtualDefinition": "$input(0)$attributes_dWMCEmailsEmail_61a9efc007907b015bb6675e$",
            "discriminator": "WorkflowVirtualItemAttributeWebModel"
        }
    ],
    "variables": []
}
```

\* This will send the same email to all the email addresses saved within the design.
However, the Recipient Name (attributes_workflowMessageActionRecipientName) can only be one for all the emails.
