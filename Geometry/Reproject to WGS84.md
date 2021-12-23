# Reproject to WGS84 (Alloy CRS)

Reproject a geometry from a different CRS to WGS84 (EPSG:4326) used by Alloy.

The **GeometryMath.ProjectToAlloyCrs()** converts from an input CRS to WGS84. Thus, it does exactly the opposite of the **GeometryMath.ProjectFromAlloyCrs()** method.\
It also makes use of the PROJ.4 conversion library to convert from an input CRS to WGS84.\
The second parameter being the PROJ.4 definition of the CRS you want to reproject from.\
PROJ.4 definitions for any CRS can be found here: [epsg.io](https://epsg.io/)

```json
{
    "parameters": [
        {
            "attributeCode": "attributes_itemsGeometry",
            "value": {
                "script": "return pointWGS84;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            },
            "discriminator": "WorkflowComputedItemAttributeWebModel"
        }
    ],
    "variables": [
        {
            "name": "pointWGS84",
            "value": {
                "script": "var point27700 = Point(Position(265740.76,431909.63)); var pointWGS84 = GeometryMath.ProjectToAlloyCrs(point27700,\"+proj=tmerc +lat_0=49 +lon_0=-2 +k=0.9996012717 +x_0=400000 +y_0=-100000 +ellps=airy +towgs84=446.448,-125.157,542.06,0.15,0.247,0.842,-20.489 +units=m +no_defs\"); return pointWGS84;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        }
    ]
}
```
#### Explanation of C# objects, methods, etc. 
- "Position(Y, X)" creates a **Position** C# object. In the example Y (Northing) and X (Easting) are the BNG coordinates of Yotta's office in Leamington.
- "Point(Position)" creates a **Point** C# object which is a Derived Class (child) of the **IGeometryObject** class
- A **Point** C# object can for example be saved in an Alloy Geometry attribute
