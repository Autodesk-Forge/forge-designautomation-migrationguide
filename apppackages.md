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

|      | V2                                                           |       | V3                                                           |
| ---- | ------------------------------------------------------------ | ----- | ------------------------------------------------------------ |
| 1    | Id -`string` unique name for AppPackage                      | 1     | id -`string` name of the AppBundle                           |
| 2    | Resource -`string` Location of the bundle containing the files to be loaded into the AutoCAD core engine | 2     | package -`string` URL that points to the zip package for the AppBundle or Engine. |
| 3    | RequiredEngineVersion -`enum:string` Version of the AutoCAD core engine to execute the AppPackage. Possible values: `22.0` | 3     | engine -`string` The actual processing engine that runs the WorkItem job and processes the Activity. |
| 4    | Version - `int` Version of the bundle referenced by the Resource attribute | 4     | refer- [AppBundle-Id-Versions](https://forge.autodesk.com/en/docs/design-automation/v3/reference/http/appbundles-id-versions-POST/) |
| 5    | Description - `string` Additional detail about the AppPackage | 5     | description - `string`                                       |
| 6    | IsPublic - `bool` Specifies whether the entity can be publicly targeted | 6     | refer - [Shares](https://forge.autodesk.com/en/docs/design-automation/v3/reference/http/shares-GET/) Sharing of AppBundles is controlled via the use of [aliases](https://forge.autodesk.com/en/docs/design-automation/v3/developers_guide/aliases-and-ids/). |
| 7    | IsObjectEnabler -`bool` Indicates whether the AppApackage represents an object enabler | 7     | n/a                                                          |
|      |                                                              | 8     | appbundles - `array:string` A module referenced by an Activity in order to perform specific functions. Typically this is a DLL or some other form of custom code |
|      |                                                              | 9     | settings - `object` The url/string Settings for a given set of AppBundles. |
|      |                                                              | 9.1   | StringSetting -`object`                                      |
|      |                                                              | 9.1.1 | value - `string`                                             |
|      |                                                              | 9.1.2 | isEnvironmentVariable -`bool`                                |
|      |                                                              | 9.2   | UrlSetting - `object`                                        |
|      |                                                              | 9.2.1 | url - `string`                                               |
|      |                                                              | 9.2.2 | headers - `object`                                           |
|      |                                                              | 9.2.3 | verb - `enum:string` The HTTP verb to be used. Possible values: `get`, `head`, `put`, `post`, `patch`, `read` |
|      |                                                              | 9.2.4 | multiparts - `object` Provide [multipart post](http://hc.apache.org/httpclient-3.x/methods/multipartpost.html) method to upload the results and multiparts can be empty if there is no “parameter” to provide. Refer [multiparts](https://forge.autodesk.com/en/docs/design-automation/v3/reference/http/activities-POST/) |



#### New POST API in V3

An AppBundle is a package of binaries and supporting files that form an AutoCAD plug-in.

You will use the following API endpoints to handle AppBundles.

| Command | Endpoint URL                                | Description                             |
| :------ | :------------------------------------------ | :-------------------------------------- |
| POST    | {baseUrl}appbundles                         | Registers a new AppBundle.              |
| POST    | {baseUrl}appbundles/{id}/aliases            | Creates a new alias for the AppBundle.  |
| POST    | {baseUrl}appbundles/{id}/versions           | Creates a new version of the AppBundle. |
| PATCH   | {baseUrl}/appbundles/{id}/aliases/{aliasId} | Modify alias details.                   |

#### Example - Post Appbundles

V2

```
curl -v 'https://developer.api.autodesk.com/autocad.io/us-east/v2/AppPackages' \
  -X 'POST' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer Js43z2DJnsYuaAxI4R2iT84b3UPy' \
  -d '
    {
      "@odata.context": "https://developer.api.autodesk.com/autocad.io/us-east/v2/$metadata#AppPackages/$entity",
      "References": [],
      "Resource": "https://acesdev.s3-us-west-2.amazonaws.com/aces-apppackages/ClientConsole-Dev/8f4cae3e-c17e-4f7a-9df9-1c4703b69889?AWSAccessKeyId=AKIAJVT56CBNM4XOWBBA&Expires=1432146217&Signature=1L%2BUF8aGM%2BZFwjHOLsxXRDQ%2FhfY%3D",
      "RequiredEngineVersion": "22.0",
      "IsPublic": false,
      "IsObjectEnabler": false,
      "Id": "SampleApp",
      "Version": 1,
      "Timestamp": "2015-02-11T19:15:40.835Z",
      "Description": ""
    }'
```

V3

```
curl -X POST \
  https://developer.api.autodesk.com/da/us-east/v3/appbundles \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -d '{
  "id": "ListLayers",
  "engine": "Autodesk.AutoCAD+22",
  "description": "List Layers AppBundle based on AutoCAD 2020"
}'
```

Refer [walk through tutorial](https://forge.autodesk.com/en/docs/design-automation/v3/tutorials/autocad/task-3-upload-appbundle/)

### Get App Bundles


|                                                              | V2                                                  | V3                                |
| ------------------------------------------------------------ | --------------------------------------------------- | --------------------------------- |
| Get All App Bundles                                          | {baseUrl}/AppPackages                               | {baseUrl}/appbundles              |
| Requests a pre-signed URL for uploading a zip file that contains the binaries for this AppPackage. | {baseUrl}/AppPackages/Operations.GetUploadUrl       | n/a                               |
| Returns the details of a specific AppPackage                 | {baseUrl}/AppPackages(‘:id’)                        | {baseUrl}/appbundles/:id          |
| Returns all old versions of a specified AppPackage.          | {baseUrl}/AppPackages(‘:id’)/Operations.GetVersions | {baseUrl}/appbundles/:id/versions |
|                                                              |                                                     |                                   |

New GET API in V3

| Command | Endpoint URL                      | Description                                    |
| :------ | :-------------------------------- | :--------------------------------------------- |
| GET     | {baseUrl}/appbundles/:id/aliases  | Lists all aliases for the specified AppBundle. |
| GET     | {baseUrl}/appbundles/:id/versions | Lists all versions of the specified AppBundle. |

#### Example: Get AppBundles\ AppPackages

V2:

```
curl -v "https://developer.api.autodesk.com/autocad.io/us-east/v2/AppPackages('SampleApp')" \
  -X 'GET' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer Ck83z2DJnsYuaAxI4R2iT84b3UPy'
```

V3: 

```
curl -v 'https://developer.api.autodesk.com/da/us-east/v3/appbundles/:id' \
  -H 'Authorization: Bearer AuIPTf4KYLTYGVnOHQ0cuolwCW2a'
```

appbundles/:id/aliases

```
curl -v 'https://developer.api.autodesk.com/da/us-east/v3/appbundles/:id/aliases' \
  -H 'Authorization: Bearer AuIPTf4KYLTYGVnOHQ0cuolwCW2a'
```

appbundles/:id/aliases/:aliasId

```
curl -v 'https://developer.api.autodesk.com/da/us-east/v3/appbundles/:id/aliases/:aliasId' \
  -H 'Authorization: Bearer AuIPTf4KYLTYGVnOHQ0cuolwCW2a'
```

appbundles/:id/versions

```
curl -v 'https://developer.api.autodesk.com/da/us-east/v3/appbundles/:id/versions' \
  -H 'Authorization: Bearer AuIPTf4KYLTYGVnOHQ0cuolwCW2a'
```

### Put, Delete, Patch Bundle

|                                                              | Command | V2                           | Command | V3                                       |
| ------------------------------------------------------------ | ------- | ---------------------------- | ------- | ---------------------------------------- |
| Updates an AppPackage by redefining the entire AppPackage object. | PUT     | {baseUrl}/AppPackages(‘:id’) | PATCH   | {baseUrl}appbundles/:id/aliases/:aliasId |
| Updates an AppPackage by specifying only the changed attributes. | PATCH   | {baseUrl}/AppPackages(‘:id’) | PATCH   | {baseUrl}appbundles/:id/aliases/:aliasId |
| Removes a specific AppPackage.                               | DELETE  | {baseUrl}/AppPackages(‘:id’) | DELETE  | {baseUrl}appbundles/:id                  |

New Delete API in V3

| Command | Endpoint URL                               | Description                                     |
| :------ | :----------------------------------------- | :---------------------------------------------- |
| DELETE  | {baseUrl}/appbundles/:id/aliases/:aliasId  | Deletes the alias.                              |
| DELETE  | {baseUrl}/appbundles/:id/versions/:version | Deletes the specified version of the AppBundle. |

#### Example : Delete App Bundles

V2

```
curl -v "https://developer.api.autodesk.com/autocad.io/us-east/v2/AppPackages('SampleApp')" \
  -X 'DELETE' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer Pt43z2DJnsYuaAxI4R2iT84b3UPy'
```

V3

```
curl -v 'https://developer.api.autodesk.com/da/us-east/v3/appbundles/:id' \
  -X 'DELETE' \
  -H 'Authorization: Bearer AuIPTf4KYLTYGVnOHQ0cuolwCW2a'
```

appbundles/:id/aliases/:aliasId

```
curl -v 'https://developer.api.autodesk.com/da/us-east/v3/appbundles/:id/aliases/:aliasId' \
  -X 'DELETE' \
  -H 'Authorization: Bearer AuIPTf4KYLTYGVnOHQ0cuolwCW2a'
```

appbundles/:id/versions/:version

```
curl -v 'https://developer.api.autodesk.com/da/us-east/v3/appbundles/:id/versions/:version' \
  -X 'DELETE' \
  -H 'Authorization: Bearer AuIPTf4KYLTYGVnOHQ0cuolwCW2a'
```