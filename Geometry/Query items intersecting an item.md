# Query items intersecting an item

Query to get all the items in a dodi that intesect with a given item (input).\

The aim is to be able to perform GIS spatial relationship operations within a workflow node.\
A customer requested this in order to get in which ward/area an asset is located.\
Afterwards the asset is assigned to a specific maintenance team based on the ward/area.


<br/>


```json
{
    "actionDesignCode": "designs_workflowOutputAction",
    "parameters": [
        {
            "attributeCode": "attributes_workflowOutputActionItems",
            "value": {
                "script": "return LOI.Take(1);",
                "returnOptions": {
                    "code": "designs_locationsOfInterest",
                    "discriminator": "DodiAttributeOptionsLinkWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        }
    ],
    "variables": [
        {
            "name": "lightingAssetID",
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
            "name": "LOI",
            "value": {
                "aqs": {
                    "type": "Query",
                    "properties": {
                        "dodiCode": "designs_locationsOfInterest",
                        "attributes": [],
                        "parameters": [
                            {
                                "name": "lightingAssetID",
                                "title": "My Parameter",
                                "type": "AlloyId"
                            }
                        ]
                    },
                    "children": [
                        {
                            "type": "And",
                            "children": [
                                {
                                    "type": "GeomIntersects",
                                    "children": [
                                        {
                                            "type": "Attribute",
                                            "properties": {
                                                "attributeCode": "attributes_itemsGeometry"
                                            }
                                        },
                                        {
                                            "type": "ValueFromItemAttribute",
                                            "properties": {
                                                "dodiCode": "designs_streetLights",
                                                "attributeCode": "attributes_itemsGeometry",
                                                "parameterName": "lightingAssetID"
                                            }
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                },
                "discriminator": "WorkflowSyntaxNodeAqsWebModel"
            }
        }
    ]
}
```
#### Explanation of C# objects, methods, etc. s
- An AQS variable is used for this purpose where the itemId of the input asset is used as AQS parameter.
- The "valueFromItemAttribute" type enables us to use an attribute (e.g. geometry) from the input asset within the query.
- The AQS variable stores the array of Alloy Item Ids returned by the query
- Using "LOI.Take(1)" and the "returnOptions" we output the first element of the array returned by the AQS
- A similar approach could be used for other spatial relationships e.g. within
