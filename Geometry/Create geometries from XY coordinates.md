# Create geometries from XY coordinates

The [GeoJSON.Net](https://github.com/GeoJSON-Net/GeoJSON.Net) library available within Workflow Computations have various C# classes and methods to build geometries from XY coordinates.

<br/>

>### Position C# class
>The fundamental geometry construct is the **Position** C# class that holds individual coordinates pairs.\
>**Position** C# objects can be initialised with "Position(Ycoord, Xcoord)" being both XY coords **doubles**.

<br/>

>### Point C# class
>**Point** C# objects can be initialised with "Point(Position)"

<br/>

>### LineString C# class
>**LineString** C# objects can be initialised by passing multiple **Positions** to "LineString(Position, Position, Position...)"

<br/>

>### Polygon C# class
>**Polygon** C# objects can be initialised by passing self-closing **LineString** (first Position = last Position) to "Polygon(LineString)"

<br/>

>### Multi Geometries
>Bulding multi geometies follow the exact same approach:\
>**MultiPoint** --> "MultiPoint(Point, Point, Point...)\
>**MultiLineString** --> "MultiLineString(LineString, LineString, LineString...)\
>**MultiPolygon** --> "MultiPolygon(Polygon, Polygon, Polygon...)

<br/>

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
        },
        {
            "name": "linestringWGS84",
            "value": {
                "script": "var linestring27700 = LineString(Position(265740.76,431909.63), Position(265820.65,431816.45)); var linestringWGS84 = GeometryMath.ProjectToAlloyCrs(linestring27700,\"+proj=tmerc +lat_0=49 +lon_0=-2 +k=0.9996012717 +x_0=400000 +y_0=-100000 +ellps=airy +towgs84=446.448,-125.157,542.06,0.15,0.247,0.842,-20.489 +units=m +no_defs\"); return linestringWGS84;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        },
        {
            "name": "polygonWGS84",
            "value": {
                "script": "var polygon27700 = Polygon(LineString(Position(265740.76,431909.63), Position(265820.65,431816.45), Position(265932.62,431966.75), Position(265740.76,431909.63))); var polygonWGS84 = GeometryMath.ProjectToAlloyCrs(polygon27700,\"+proj=tmerc +lat_0=49 +lon_0=-2 +k=0.9996012717 +x_0=400000 +y_0=-100000 +ellps=airy +towgs84=446.448,-125.157,542.06,0.15,0.247,0.842,-20.489 +units=m +no_defs\"); return polygonWGS84;",
                "discriminator": "WorkflowSyntaxNodeScriptWebModel"
            }
        }
    ]
}
```
