# Buffer to get closest item to another item

In some scenarios is useful to be able to compute which item is closest to another item. 
For example:
- Link a Gully asset to the closest street asset 
- Find the CW inspection details closest to a defect
- Find the SC section closest to a fly tip defect
- etc.

In theses cases you can use a computed Output node with the following logic:
- converts geometry of the origin item (the one for which you want to find the closest item) to WGS84
- create various variables each one with computed buffer areas with different radius (e.g. 1m, 5m, 10m, 20m, etc.)
- use each buffer in an AQS query variable (destination item within buffer area of the origin item)
- add computed logic to check if the AQS returns destination items, starting from the smallest to the biggest buffer.
- output the first destination item found (the closest one)


```json
{
  "actionDesignCode": "designs_workflowOutputAction",
  "ancestorId": "67361df649775d8f13eb33b9",
  "signature": "6749bde8cc7b3e804673ab5b",
  "description": "Get Closest Manual Sweep SC Section",
  "parameters": [
    {
      "attributeCode": "attributes_workflowOutputActionItems",
      "value": {
        "script": "var output = sc_section_5m.Take(1); if( sc_section_5m.Count() > 0 ){ output = sc_section_5m.Take(1); } else if( sc_section_10m.Count() > 0 ){ output = sc_section_10m.Take(1); } else if( sc_section_20m.Count() > 0 ){ output = sc_section_20m.Take(1); } else if ( sc_section_30m.Count() > 0 ){ output = sc_section_30m.Take(1); } else if( sc_section_40m.Count() > 0 ){ output = sc_section_40m.Take(1); } else if( sc_section_50m.Count() > 0 ){ output = sc_section_50m.Take(1); } ; return output;",
        "returnOptions": {
          "code": "designs_streetCleansingSection_655c83487e00116850fda33b",
          "weakReference": false,
          "defaultValue": [],
          "discriminator": "DodiAttributeOptionsLinkWebModel"
        },
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
      },
      "discriminator": "WorkflowComputedItemAttributeWebModel"
    }
  ],
  "variables": [
    {
      "name": "geometry_WGS84",
      "value": {
        "inputParent": 0,
        "itemValue": {
          "attributeCode": "attributes_itemsGeometry",
          "discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
        },
        "discriminator": "WorkflowSyntaxNodeInputWebModel"
      }
    },
    {
      "name": "geometry_BNG",
      "value": {
        "script": "var geometry_BNG = GeometryMath.ProjectFromAlloyCrs(geometry_WGS84,\"+proj=tmerc +lat_0=49 +lon_0=-2 +k=0.9996012717 +x_0=400000 +y_0=-100000 +ellps=airy +towgs84=446.448,-125.157,542.06,0.15,0.247,0.842,-20.489 +units=m +no_defs\");return geometry_BNG;",
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
      }
    },
    {
      "name": "buffer_5m_WGS84",
      "value": {
        "script": "var radius = 5; return GeometryMath.ProjectToAlloyCrs(GeometryMath.Buffer(radius, geometry_BNG),\"+proj=tmerc +lat_0=49 +lon_0=-2 +k=0.9996012717 +x_0=400000 +y_0=-100000 +ellps=airy +towgs84=446.448,-125.157,542.06,0.15,0.247,0.842,-20.489 +units=m +no_defs\");",
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
      }
    },
    {
      "name": "buffer_10m_WGS84",
      "value": {
        "script": "var radius = 10; return GeometryMath.ProjectToAlloyCrs(GeometryMath.Buffer(radius, geometry_BNG),\"+proj=tmerc +lat_0=49 +lon_0=-2 +k=0.9996012717 +x_0=400000 +y_0=-100000 +ellps=airy +towgs84=446.448,-125.157,542.06,0.15,0.247,0.842,-20.489 +units=m +no_defs\");",
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
      }
    },
    {
      "name": "buffer_20m_WGS84",
      "value": {
        "script": "var radius = 20; return GeometryMath.ProjectToAlloyCrs(GeometryMath.Buffer(radius, geometry_BNG),\"+proj=tmerc +lat_0=49 +lon_0=-2 +k=0.9996012717 +x_0=400000 +y_0=-100000 +ellps=airy +towgs84=446.448,-125.157,542.06,0.15,0.247,0.842,-20.489 +units=m +no_defs\");",
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
      }
    },
    {
      "name": "buffer_30m_WGS84",
      "value": {
        "script": "var radius = 30; return GeometryMath.ProjectToAlloyCrs(GeometryMath.Buffer(radius, geometry_BNG),\"+proj=tmerc +lat_0=49 +lon_0=-2 +k=0.9996012717 +x_0=400000 +y_0=-100000 +ellps=airy +towgs84=446.448,-125.157,542.06,0.15,0.247,0.842,-20.489 +units=m +no_defs\");",
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
      }
    },
    {
      "name": "buffer_40m_WGS84",
      "value": {
        "script": "var radius = 40; return GeometryMath.ProjectToAlloyCrs(GeometryMath.Buffer(radius, geometry_BNG),\"+proj=tmerc +lat_0=49 +lon_0=-2 +k=0.9996012717 +x_0=400000 +y_0=-100000 +ellps=airy +towgs84=446.448,-125.157,542.06,0.15,0.247,0.842,-20.489 +units=m +no_defs\");",
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
      }
    },
    {
      "name": "buffer_50m_WGS84",
      "value": {
        "script": "var radius = 50; return GeometryMath.ProjectToAlloyCrs(GeometryMath.Buffer(radius, geometry_BNG),\"+proj=tmerc +lat_0=49 +lon_0=-2 +k=0.9996012717 +x_0=400000 +y_0=-100000 +ellps=airy +towgs84=446.448,-125.157,542.06,0.15,0.247,0.842,-20.489 +units=m +no_defs\");",
        "discriminator": "WorkflowSyntaxNodeScriptWebModel"
      }
    },
    {
      "name": "sc_section_5m",
      "value": {
        "aqs": {
          "type": "Query",
          "properties": {
            "collectionCode": [
              "Live"
            ],
            "dodiCode": "designs_streetCleansingSection_655c83487e00116850fda33b",
            "parameters": [
              {
                "name": "buffer_5m_WGS84",
                "type": "Geometry",
                "title": "buffer_5m_WGS84"
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
                      "type": "Geometry",
                      "properties": {
                        "parameterName": "buffer_5m_WGS84"
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
    },
    {
      "name": "sc_section_10m",
      "value": {
        "aqs": {
          "type": "Query",
          "properties": {
            "collectionCode": [
              "Live"
            ],
            "dodiCode": "designs_streetCleansingSection_655c83487e00116850fda33b",
            "parameters": [
              {
                "name": "buffer_10m_WGS84",
                "type": "Geometry",
                "title": "buffer_10m_WGS84"
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
                      "type": "Geometry",
                      "properties": {
                        "parameterName": "buffer_10m_WGS84"
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
    },
    {
      "name": "sc_section_20m",
      "value": {
        "aqs": {
          "type": "Query",
          "properties": {
            "collectionCode": [
              "Live"
            ],
            "dodiCode": "designs_streetCleansingSection_655c83487e00116850fda33b",
            "parameters": [
              {
                "name": "buffer_20m_WGS84",
                "type": "Geometry",
                "title": "buffer_20m_WGS84"
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
                      "type": "Geometry",
                      "properties": {
                        "parameterName": "buffer_20m_WGS84"
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
    },
    {
      "name": "sc_section_30m",
      "value": {
        "aqs": {
          "type": "Query",
          "properties": {
            "collectionCode": [
              "Live"
            ],
            "dodiCode": "designs_streetCleansingSection_655c83487e00116850fda33b",
            "parameters": [
              {
                "name": "buffer_30m_WGS84",
                "type": "Geometry",
                "title": "buffer_30m_WGS84"
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
                      "type": "Geometry",
                      "properties": {
                        "parameterName": "buffer_30m_WGS84"
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
    },
    {
      "name": "sc_section_40m",
      "value": {
        "aqs": {
          "type": "Query",
          "properties": {
            "collectionCode": [
              "Live"
            ],
            "dodiCode": "designs_streetCleansingSection_655c83487e00116850fda33b",
            "parameters": [
              {
                "name": "buffer_40m_WGS84",
                "type": "Geometry",
                "title": "buffer_40m_WGS84"
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
                      "type": "Geometry",
                      "properties": {
                        "parameterName": "buffer_40m_WGS84"
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
    },
    {
      "name": "sc_section_50m",
      "value": {
        "aqs": {
          "type": "Query",
          "properties": {
            "collectionCode": [
              "Live"
            ],
            "dodiCode": "designs_streetCleansingSection_655c83487e00116850fda33b",
            "parameters": [
              {
                "name": "buffer_50m_WGS84",
                "type": "Geometry",
                "title": "buffer_50m_WGS84"
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
                      "type": "Geometry",
                      "properties": {
                        "parameterName": "buffer_50m_WGS84"
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
