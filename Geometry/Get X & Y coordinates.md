# Get X & Y coordinates

Get and store X (longitude, easting, etc.) and Y (latitude, northing, etc.) coordinates from an input geomtry into 2 number attributes.

The [GeoJSON.Net](https://github.com/GeoJSON-Net/GeoJSON.Net) library available within Workflow Computations have various C# classes, methods, properties, etc. that are of help for this case.

<br/>


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
            "name": "geometryWGS84",
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
            "name": "latitude",
            "value": {
                "script": "var existingPoint = geometryWGS84 as GeoJSON.Net.Geometry.Point; var latitude = existingPoint.Coordinates.Latitude; return latitude;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "longitude",
            "value": {
                "script": "var existingPoint = geometryWGS84 as GeoJSON.Net.Geometry.Point; var longitude = existingPoint.Coordinates.Longitude; return longitude;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        }
    ]
}
```
#### Explanation of C# objects, methods, etc. s
- "geometryWGS84" is a **IGeometryObject** C# object
- With "as GeoJSON.Net.Geometry.Point" we explicitly cast/convert from **IGeometryObject** (any geometry) to a **Point**.
In order for this to work you need to make sure that the input geometry is a point.
- "Point.Coordinates" and "Point.Coordinates.Latitude/Longitude" are available **Point** properties
