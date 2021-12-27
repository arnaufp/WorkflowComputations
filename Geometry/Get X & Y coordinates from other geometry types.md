# Get X & Y coordinates from other geometry types (Centroid)

Getting one X & Y coordinate pair from non-Point geometries can be achieve by using the "Centroid()" function and then the Lat/Lon of it. 
Though the resulting centroid point and XY coordinate might not overlap the original geometry:

[<img src="http://www.orbital.co.ke:8080/opengeo-docs/_images/centroid.png">](#)


```json
{
    "parameters": [
        {
            "attributeCode": "attributes_testJobLatitude_602f998f39e0d6006aef689d",
            "value": {
                "script": "return latitude;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        },
        {
            "attributeCode": "attributes_testJobLongitude_602e84b756a33800665e5d3c",
            "value": {
                "script": "return longitude;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        }
    ],
    "variables": [
        {
            "name": "inputGeometry",
            "value": {
                "inputParent": 0,
                "itemValue": {
                    "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel",
                    "attributeCode": "attributes_itemsGeometry"
                },
                "discriminator": "WorkflowSyntaxNodeInputWebModel"
            }
        },
        {
            "name": "centroid",
            "value": {
                "script": "var centroid = GeometryMath.Centroid(inputGeometry); return centroid;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "latitude",
            "value": {
                "script": "var c = centroid as GeoJSON.Net.Geometry.Point; return c.Coordinates.Latitude;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "longitude",
            "value": {
                "script": "var c = centroid as GeoJSON.Net.Geometry.Point; return c.Coordinates.Longitude;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        }
    ]
}
```

Getting a XY coordinate pair that surely overlays with the original geometry can be achieved by following various approaches:
- get the first coordinate pair of the original geometry
- get the last coordinate pair of the original geometry
- Etc.
