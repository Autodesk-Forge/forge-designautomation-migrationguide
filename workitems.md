## Workitems

 A job that is submitted to and executed by the AutoCAD core engine. A WorkItem is used to execute an Activity; the relationship between an Activity and WorkItem can be thought of as a “function definition” and “function call”, respectively.

*Note: Once a WorkItem is created, it cannot be modified.*

| API Spec | Description | V2                                                           | V3                                                           |
| :------- | ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| WorkItem | Base URL    | POSThttps://developer.api.autodesk.com/autocad.io/us-east/v2 | https://developer.api.autodesk.com/da/us-east/v3             |
|          |             |                                                              | No of Activities that can be created -1, limit varies by Engine. |

### Headers

|                   | v2                                                           | v3        |
| ----------------- | ------------------------------------------------------------ | --------- |
| **Authorization** | Must be `Bearer `, where `token` is obtained via [OAuth](https://forge.autodesk.com/en/docs/oauth/v2/reference/http/authenticate-POST) | No Change |
| **Content-Type**  | Must be `application/json`                                   | No Change |

### Body

|                 | V2                                                           |      | V3                                                           |
| --------------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| URL             | https://developer.api.autodesk.com/autocad.io/us-east/v2/WorkItems |      | POSThttps://developer.api.autodesk.com/da/us-east/v3/workitems |
| Body Attributes |                                                              |      |                                                              |
| 1               | ActivityId -`string`                                         |      | activityId                                                   |
| 2               | Arguments -`object`                                          |      | arguments                                                    |
| 2.1             | InputArguments -`object`                                     |      |                                                              |
| 2.1.1           | Resource -`string`                                           |      |                                                              |
| 2.1.2           | Name - `string`                                              |      |                                                              |
| 2.1.3           | Headers - `array:string`                                     |      |                                                              |
| 2.1.4           | ResourceKind -`enum:string`                                  |      |                                                              |
| 2.1.5           | StorageProvider-`string`                                     |      |                                                              |
| 2.1.6           | HttpVerb-`enum:string`                                       |      |                                                              |
| 2.2             | OutputArguments -`object`                                    |      |                                                              |
| 2..2.1          | Resource -`string`                                           |      |                                                              |
|                 | Name - `string`                                              |      |                                                              |
|                 | Headers - `array:string`                                     |      |                                                              |
|                 |                                                              |      |                                                              |
|                 |                                                              |      |                                                              |
|                 |                                                              |      |                                                              |

