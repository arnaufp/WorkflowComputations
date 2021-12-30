# Workflow Computations

This repository is intended to store and be used as a reference library for any useful workflow computation as well as their related C# scripts, use cases that solves, workflow diagram screenshots or any other relevant information.

Therefore, the aim is to document:
- Basic or generic computations that others can easily search for and reuse 
- As well as more bespoke solutions that could be slightly changed to be reused by other customers

### Basic Syntax (copy/paste & go)
- [Variables](Basic%20Syntax/Variables.md)
- [Parameters](Basic%20Syntax/Parameters.md)

### Geometry
- [Reproject from WGS84 (Alloy CRS)](Geometry/Reproject%20from%20WGS84.md)
- [Reproject to WGS84 (Alloy CRS)](Geometry/Reproject%20to%20WGS84.md)
- [Create geometries from XY coordinates](Geometry/Create%20geometries%20from%20XY%20coordinates.md)
- [Merge geometries into a Geometry Collection](Geometry/Merge%20geometries%20into%20a%20Geometry%20Collection.md)
- [Get X & Y coordinates from a point](Geometry/Get%20X%20&%20Y%20coordinates%20from%20a%20point.md)
- [Get X & Y coordinates from other geometry types (Centroid)](Geometry/Get%20X%20&%20Y%20coordinates%20from%20other%20geometry%20types.md)
- [Polygon to LineString](Geometry/Polygon%20to%20LineString.md)
- [Area & Length](Geometry/Area%20%26%20Length.md)
- [Query items intersecting an item](Geometry/Query%20items%20intersecting%20an%20item.md)
- Buffer related
- Bounding Box related
- Create tree canopy geometries
- Other conversions between different geometry types

### Date & Time
- [DateTime attribute to day of the week](Dates/DateTime%20attribute%20to%20day%20of%20the%20week.md)
- [DateTime attribute to Date and Time attributes](Dates/DateTime%20attribute%20to%20Date%20and%20Time%20attributes.md)
- [DateTime attribute falls on a weekend?](Dates/DateTime%20attribute%20falls%20on%20a%20weekend%3F.md)
- [Duration between 2 DateTime attributes](Dates/Duration%20between%202%20DateTime%20attributes.md)
- [Calculate next cyclic maintenance due dates](Dates/Calculate%20next%20cyclic%20maintenance%20due%20dates.md)
- [Target Time = Raised Time + Working Hours Offset](Dates/Target%20Time%20=%20Raised%20Time%20+%20Working%20Days%20Offset.md)
- Other datetime available operations, conversions, etc.

### Messaging (email, sms, http requests)
- Set HTTP Request example
- Set multiple HTTP headers
- Set custom email
- Set custom sms

### Others
- Unset attributes
- modify / manipulate a json attribute
- Archive project once all tasks are completed
- Task performance indicators
- Count & send: defect counter against assets + issue emails when counter is multiple of 5
- Compute the Carbon Footprint of operatives
