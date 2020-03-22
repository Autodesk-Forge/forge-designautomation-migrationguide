## Activities

The specification of an action that can be executed using a specified engine.

For example, using AutoCAD to plot a supplied DWG to a PDF file. Another example: using AutoCAD to update a supplied DWG file to use a different set of CAD standards.



| API Spec | Description | V2                                                       | V3                                                           |
| :------- | ----------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| Activity | Base URL    | https://developer.api.autodesk.com/autocad.io/us-east/v2 | https://developer.api.autodesk.com/da/us-east/v3             |
|          |             |                                                          | No of Activities that can be created -1, limit varies by Engine. |

#### Headers

|                   | v2                                                           | v3        |
| ----------------- | ------------------------------------------------------------ | --------- |
| **Authorization** | Must be `Bearer <token> `, where `token` is obtained via [OAuth](https://forge.autodesk.com/en/docs/oauth/v2/reference/http/authenticate-POST) | No Change |
| **Content-Type**  | Must be `application/json`                                   | No Change |



| API             | V2                                                           |       | V3                                                           |
| --------------- | ------------------------------------------------------------ | ----- | ------------------------------------------------------------ |
| URL             | https://developer.api.autodesk.com/autocad.io/us-east/v2/Activities |       | https://developer.api.autodesk.com/da/us-east/v3/activities  |
| Body Attributes |                                                              |       |                                                              |
| 1               | AppPackages                                                  | 1     | appbundles                                                   |
| 2               | HostApplication                                              | 2     | n/a                                                          |
| 3               | RequiredEngineVersion                                        | 3     | engine                                                       |
| 4               | Parameters                                                   | 4     | parameters                                                   |
| 4.1             | InputParameters                                              | 4.1   | zip -` boolean`                                              |
| 4.1.1           | Name                                                         | 4.2   | ondemand -`boolean`                                          |
| 4.1.2           | LocalFileName                                                | 4.3   | verb  -`get`, `head`, `put`, `post`, `patch`, `read`         |
| 4.1.3           | Optional                                                     | 4.4   | description - `string`, description of the parameter         |
| 4.2             | OutputParameters                                             | 4.5   | required -`boolean`                                          |
| 4.2.1           | Name                                                         | 4.6   | localname-`string`                                           |
| 4.2.2           | LocalFileName                                                |       |                                                              |
| 4.2.3           | Optional                                                     |       |                                                              |
| 5               | Id                                                           | 5     | id -`string`                                                 |
| 6               | Instruction                                                  | 6     | commandLine -`The command run by this Activity`              |
| 6.1             | CommandLineParameters                                        | 6.1   | settings -`Contains the script to be run by the AutoCAD engine, as referred to in commandLine` |
| 6.2             | Script                                                       | 6.1.1 | script -`A script is a text file with command or a script call on each line.` |
| 7               | AllowedChildProcesses                                        | 7     | n\a                                                          |
| 8               | Version                                                      | 8     | {baseUrl}/v3/activities/{id}/versions -[Assign an existing alias to the updated Activit](https://forge.autodesk.com/en/docs/design-automation/v3/tutorials/autocad/task-4-publish-activity/#step-4-assign-an-existing-alias-to-the-updated-activity) |
| 9               | Description                                                  | 9     | description -`string`, description of the activity           |
| 10              | IsPublic                                                     | 10    | n\a                                                          |
|                 |                                                              |       |                                                              |
|                 |                                                              |       |                                                              |

