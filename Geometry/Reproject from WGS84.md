# Reproject from WGS84 (Alloy CRS)

Reproject "attributes_itemsGeometry" which use WGS84 (EPSG:4236) to another CRS.

The **GeometryMath.ProjectFromAlloyCrs()** method makes use of the PROJ.4 conversion library to convert from WGS84 to another CRS.\
The second parameter being the PROJ.4 definition of the CRS you want to reproject to.\
PROJ.4 definitions for any CRS can be found here: [epsg.io](https://epsg.io/)

```json
{
    "parameters": [
        {
            "attributeCode": "attributes_streetLightsBNGGeoJson_5fc7b0850b95140064ab52b6",
            "value": {
                "script": "var geometryBNG = GeometryMath.ProjectFromAlloyCrs(geometryWGS84,\"+proj=tmerc +lat_0=49 +lon_0=-2 +k=0.9996012717 +x_0=400000 +y_0=-100000 +ellps=airy +towgs84=446.448,-125.157,542.06,0.15,0.247,0.842,-20.489 +units=m +no_defs\");return Json(geometryBNG);",
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
- "geometryWGS84" is a **IGeometryObject** C# object
- "geometryBNG" is a **IGeometryObject** C# object
- "Json(geometryBNG)" converts it to a **JObject** C# object
- A **JObject** can for example be saved in an Alloy JSON attribute
