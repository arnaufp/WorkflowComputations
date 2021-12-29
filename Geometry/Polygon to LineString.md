# Polygon to LineString

Convert a Polygon to a LineString and save it back to attributes_itemsGeometry

<br/>

```json
{
    "parameters": [
        {
            "attributeCode": "attributes_itemsGeometry",
            "value": {
                "script": "return linestring;",
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
            "name": "linestring",
            "value": {
                "script": "var polygon = inputGeometry as GeoJSON.Net.Geometry.Polygon; var jsonPolygon = Json(polygon); var coordinates = jsonPolygon[\"coordinates\"][0]; var coordinatesArray = coordinates.ToArray(); var positions = coordinatesArray.Select(p => Position((double)p[1], (double)p[0])); var linestring = LineString(positions.ToArray()); return linestring ;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        }
    ]
}
```
#### Explanation of C# objects, methods, etc.
- "geometryWGS84" is a **IGeometryObject** C# object
- With "as GeoJSON.Net.Geometry.Polygon" we explicitly cast/convert from **IGeometryObject** (any geometry) to a **Polygon**.
In order for this to work you need to make sure that the input geometry is a polygon.
- "Json(polygon)" converts it to a **JObject** C# object. So that we can access specific JSON keys such as "jsonPolygon[\"coordinates\"][0]"
- "coordinates.ToArray()" converts to an array e.g. [[1.0, 51.0], [2.0, 51.0], [2.0, 52.0], [1.0, 52.0], [1.0, 51.0]]
- ".Select()" allows you to transform (project) each element of a sequence into a new form
- Using ".Select(p => Position((double)p[1], (double)p[0]))" we transform each element into a **Position**
- "Linestring()" requires an array of **Positions** to convert them to a **LineString** C# object

*This might only work with regular Polygons (without inner rings or holes)
