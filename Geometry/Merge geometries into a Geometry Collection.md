# Merge geometries into a Geometry Collection

### Customer request (Plymouth): 

Asset1 can be linked to many Asset2 children. When an Asset1 is created and the Asset2 children are linked, Asset1 should take the merged geometry of all their children. 
The geometry of Asset2 items can be anything: Point, LineString, Polygon, etc., thus the resulting geometry must be a Geometry Collection

### Solution
This requires minimum 3 Workflow Nodes:
1. A first node that outputs Asset1
2. A Relation node connected to node 1 that outputs all the linked Asset2 items
3. A computed Edit Node connected to node 1 that uses the items outputted by node 2, computed the new geometry and updates Asset1

<br/>

>### GeometryCollection C# class
>A **GeometryCollection** C# object can be initialised by passing an array of **IGeometryObject** C# objects to "GeometryCollection(IGeometryObject[])"

<br/>

```json
{
    "parameters": [
        {
            "attributeCode": "attributes_itemsGeometry",
            "value": {
                "script": "return geometryCollection;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        }
    ],
    "variables": [
        {
            "name": "geometries",
            "value": {
                "outputAction": "61a0afc64ad2e7015a380e6d",
                "itemValue": {
                    "attributeCode": "attributes_itemsGeometry",
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
                },
                "discriminator": "WorkflowSyntaxNodeOutputWebModel"
            }
        },
        {
            "name": "geometryCollection",
            "value": {
                "script": "return GeometryCollection(Variables.geometries.AllValues.Values.Select(x => x.SingleValue).ToArray());",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        }
    ]
}
```
