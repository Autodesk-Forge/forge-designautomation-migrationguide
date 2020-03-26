## AppPackages

A module referenced by an Activity in order to perform specific functions. Typically this is a DLL or some other form of custom code.

For example, using the AutoCAD engine, this might be a custom AutoLISP routine that extracts Xdata attached to objects in a drawing or a script file that plots a DWG to a PDF file.



| API Spec             | Description | V2                                                           | V3                                                           |
| :------------------- | ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| AppPackage/AppBundle | Base URL    | https://developer.api.autodesk.com/autocad.io/us-east/v2     | https://developer.api.autodesk.com/da/us-east/v3             |
|                      |             | Creates an AppPackage module.                                | Creates a new AppBundle.                                     |
|                      |             | Before an AppPackage object can be created, you must make a request for a pre-signed URL that will be used to upload the module file. | Limits: (varies by Engine)<br/>1. Number of AppBundle that can be created.<br/>2. Size of AppBundle.<br/>This method creates new AppBundle returned in response value.<br/>POST upload is required to limit upload size.<br/><br/>After this request, you need to upload the AppBundle zip.<br/>To upload the AppBundle package, create a multipart/form-data request using data received in reponse uploadParameters:<br/>- endpointURL is the URL to make the upload package request against,<br/>- formData are the parameters that need to be put into the upload package request body.<br/>They must be followed by an extra ‘file’ parameter indicating the location of the package file.<br/>An example:<br/><br/>curl https://bucketname.s3.amazonaws.com/<br/>-F key = apps/myApp/myfile.zip<br/>-F content-type = application/octet-stream<br/>-F policy = eyJleHBpcmF0aW9uIjoiMjAxOC0wNi0yMVQxMzo...(trimmed)<br/>-F x-amz-signature = 800e52d73579387757e1c1cd88762...(trimmed)<br/>-F x-amz-credential = AKIAIOSFODNN7EXAMPLE/20180621/us-west-2/s3/aws4_request/<br/>-F x-amz-algorithm = AWS4-HMAC-SHA256<br/>-F x-amz-date = 20180621T091656Z<br/>-F file=@E:myfile.zip<br/>The ‘file’ field must be at the end, all fields after ‘file’ will be ignored. |

### Headers

|                   | v2                                                           | v3        |
| ----------------- | ------------------------------------------------------------ | --------- |
| **Authorization** | Must be `Bearer `, where `token` is obtained via [OAuth](https://forge.autodesk.com/en/docs/oauth/v2/reference/http/authenticate-POST) | No Change |
| **Content-Type**  | Must be `application/json`                                   | No Change |

### Body 

|      | V2                                                           |      | V3                                                           |
| ---- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| 1    | Id -`string` unique name for AppPackage                      | 1    | id -`string` name of the AppBundle                           |
| 2    | Resource -`string` Location of the bundle containing the files to be loaded into the AutoCAD core engine | 2    | package -`string` URL that points to the zip package for the AppBundle or Engine. |
| 3    | RequiredEngineVersion -`enum:string` Version of the AutoCAD core engine to execute the AppPackage. Possible values: `22.0` | 3    | engine -`string` The actual processing engine that runs the WorkItem job and processes the Activity. |
| 4    |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |
|      |                                                              |      |                                                              |

