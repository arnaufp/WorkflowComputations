# HTTP Request with multiple headers

It could be that more than one HTTP Header must be configured as part of the WebHook or HTTP Request node.\
This can be easily achieved by adding a new line character (\n) in between each pair of headers. \
See value of "attributes_workflowHttpRequestActionsHttpHeaders":

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
                "value": "Content-Type: application/json\nSecond-Header: header2"
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
                "template": "{\"message\": \"job completed\"}",
                "discriminator": "WorkflowSyntaxNodeTemplateWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        }
    ],
    "variables": []
}
```

As a result, once the HTTP Request node is executed you will get the following:
```
POST / HTTP/1.1
Host: blackburn2.requestcatcher.com
Connection: Keep-Alive
Content-Length: 28
Content-Type: application/json
Second-Header: header2

{"message": "job completed"}
```
