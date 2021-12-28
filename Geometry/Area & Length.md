# Area & Length

Compute Area & Length of input geometries (attributes_itemsGeometry)

<br/>

>### Area
> - Polygon, MultiPolygon and GeometryCollection

```json
{
    "parameters": [
        {
            "attributeCode": "attributes_demoAssetArea_5f52693b72b4d50065a614e5",
            "value": {
                "script": "var geometryBNG = GeometryMath.ProjectFromAlloyCrs(geometryWGS84,\"+proj=tmerc +lat_0=49 +lon_0=-2 +k=0.9996012717 +x_0=400000 +y_0=-100000 +ellps=airy +towgs84=446.448,-125.157,542.06,0.15,0.247,0.842,-20.489 +units=m +no_defs\");return GeometryMath.Area(geometryBNG);",
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
        }
    ]
}
```

<br/>
<br/>

>### Length
> - LineString, MultiLineString --> length
> - Polygon, MultiPolygon --> perimeter
```json
{
    "parameters": [
        {
            "attributeCode": "attributes_demoAssetLength_5f52693b72b4d50065a614e5",
            "value": {
                "script": "var geometryBNG = GeometryMath.ProjectFromAlloyCrs(geometryWGS84,\"+proj=tmerc +lat_0=49 +lon_0=-2 +k=0.9996012717 +x_0=400000 +y_0=-100000 +ellps=airy +towgs84=446.448,-125.157,542.06,0.15,0.247,0.842,-20.489 +units=m +no_defs\");return GeometryMath.Length(geometryBNG);",
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
        }
    ]
}
```
#### Explanation of C# objects, methods, etc. 
- It is recommended to use a projected CRS when doing geometric operations. 
- Thus it is a good practice to project the incoming geometries (WGS84) to a local coordinate system that measures in metres. 
- EPSG:27700 it is normally a good choice, though EPSG:27700 is neither equal-area (preserve area) nor equidistant (preserve distances) but a conformal (preserve shapes) projection 
- "GeometryMath.ProjectFromAlloyCrs(**IGeometryObject**, **PROJ.4 string**)" converts to the local EPSG:27700 CRS
- "GeometryMath.Length(**IGeometryObject**)" returns the length in the CRS units
- "GeometryMath.Area(**IGeometryObject**)" returns the area in the CRS units
