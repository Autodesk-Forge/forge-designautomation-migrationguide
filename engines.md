## Engine

The actual processing engine that runs the WorkItem job and processes the Activity. In V3, the following engine types are available:
 - AutoCAD
 - 3dsMax 
 - Inventor 
 - Revit 

Note: There may be multiple versions of each engine.

| API Spec | Description | V2                                                       | V3                                               |
| -------- | ----------- | -------------------------------------------------------- | ------------------------------------------------ |
| Engine   | baseUrl     | https://developer.api.autodesk.com/autocad.io/us-east/v2 | https://developer.api.autodesk.com/da/us-east/v3 |

### Headers

|                   | v2                                                           | v3        |
| ----------------- | ------------------------------------------------------------ | --------- |
| **Authorization** | Must be `Bearer `, where `token` is obtained via [OAuth](https://forge.autodesk.com/en/docs/oauth/v2/reference/http/authenticate-POST) | No Change |

### Get Engines

|                                                        | V2                       | V3                                                           |
| ------------------------------------------------------ | ------------------------ | ------------------------------------------------------------ |
| Lists all available Engines                            | {baseUrl}/Engines        | {baseUrl}/engines                                            |
| Returns the details of a specific AutoCAD core engine. | {baseUrl}/Engines(‘:id’) | {baseUrl}/engines/:id <br />`:id` Full qualified id of the Engine (owner.name+label). |

#### Example: Get Engines

V2

```
curl -v "https://developer.api.autodesk.com/autocad.io/us-east/v2/Engines('22.0')" \
  -X 'GET' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer Ck83z2DJnsYuaAxI4R2iT84b3UPy' \
```

V3

```
curl -v 'https://developer.api.autodesk.com/da/us-east/v3/engines/Autodesk.AutoCAD+22' \
  -H 'Authorization: Bearer AuIPTf4KYLTYGVnOHQ0cuolwCW2a'
```