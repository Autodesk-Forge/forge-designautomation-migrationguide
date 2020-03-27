## Workitems

 A job that is submitted to and executed by the AutoCAD core engine. A WorkItem is used to execute an Activity; the relationship between an Activity and WorkItem can be thought of as a “function definition” and “function call”, respectively.

*Note: Once a WorkItem is created, it cannot be modified.*

| API Spec | Description | V2                                                       | V3                                                           |
| :------- | ----------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| WorkItem | Base URL    | https://developer.api.autodesk.com/autocad.io/us-east/v2 | https://developer.api.autodesk.com/da/us-east/v3             |
|          |             |                                                          | The new WorkItem is always placed on a queue and later picked up by an engine.<br />Per-engine. These limits are enforced when the engine processes the workitem.<br />- Number of downloads (LimitDownloads)<br/>- Number of uploads (LimitUploads)<br/>- Total download size (LimitDownloadSize)<br/>- Total upload size (LimitUploadSize)<br/>- Processing time (LimitProcessingTime)<br/>- Total size of uncompressed bits for all referenced appbundles (LimitTotalUncompressedAppsSizePerActivity). |

### |Headers

|                   | v2                                                           | v3        |
| ----------------- | ------------------------------------------------------------ | --------- |
| **Authorization** | Must be `Bearer `, where `token` is obtained via [OAuth](https://forge.autodesk.com/en/docs/oauth/v2/reference/http/authenticate-POST) | No Change |
| **Content-Type**  | Must be `application/json`                                   | No Change |

### Body

A simple description is given for each attribute in V3 body structure, for detailed documentation refer [v3-post-workItems](https://forge.autodesk.com/en/docs/design-automation/v3/reference/http/workitems-POST/) documentation.



|                 | V2                                                           |       | V3                                                           |
| --------------- | ------------------------------------------------------------ | ----- | ------------------------------------------------------------ |
| URL             | https://developer.api.autodesk.com/autocad.io/us-east/v2/WorkItems |       | POSThttps://developer.api.autodesk.com/da/us-east/v3/workitems |
| Body Attributes |                                                              |       |                                                              |
| 1               | ActivityId -`string`                                         | 1     | activityId -`string`                                         |
| 2               | Arguments -`object`                                          | 2     | arguments -`object`                                          |
| 2.1             | InputArguments -`object`                                     | 2.1   | StringArgument -`object` <br />Simple string argument. This class represents string argument both in the workitem and job. |
| 2.1.1           | Resource -`string`                                           | 2.1.1 | value -`string`                                              |
| 2.1.2           | Name - `string`                                              | 2.2   | XrefTreeArgument - `object`<br />Represents an HTTP request argument in the workitem |
| 2.1.3           | Headers - `array:string`                                     | 2.2.1 | optional - `boolean`  Defaults to false.<br />Failure to download optional input arguments is OK. Failure to find or upload optional output arguments is OK. |
| 2.1.4           | ResourceKind -`enum:string`                                  | 2.2.2 | localName -`string` <br />Provides default name of the file or folder on the processing server for this argument |
| 2.1.5           | StorageProvider-`string`                                     | 2.2.3 | pathInZip - string <br />Denotes the “main file” in a zip. This attribute together with the Autodesk.Das.Shared.Models.Parameter.Zip attribute determine how zip files are handled. |
| 2.1.6           | HttpVerb-`enum:string`                                       | 2.2.4 | references - `array`                                         |
| 2.2             | OutputArguments -`object`                                    | 2.2.5 | url  -`string`                                               |
| 2..2.1          | Resource -`string`                                           | 2.2.6 | headers - `object` Headers                                   |
| 2.2.2           | Name - `string`                                              | 2.2.7 | verb -`enum:string` <br />The HTTP verb to be used. Possible values: `get`, `head`, `put`, `post`, `patch`, `read` |
| 2.2.3           | Headers - `array:string`                                     | 2.2.8 | multiparts -`object`<br />Provide [multipart post](http://hc.apache.org/httpclient-3.x/methods/multipartpost.html) method to upload the results and multiparts can be empty if there is no “parameter” to provide. It supports Box, Google Drive, AWS S3 |
| 2.2.4           | ResourceKind -`enum:string`                                  | 3     | signatures -`object` Signatures for various WorkItem attributes. |
| 2.2.5           | StorageProvider-`string`                                     | 3.1   | activityId -`string` Digital signature of the ActivityId. The client must supply this when using a 3-legged oauth token for submitting a WorkItem. |
| 2.2.6           | HttpVerb-`enum:string`                                       | 3.2   | baseUrls - `array:object` Digitally signed base urls that are allowed in the WorkItem. The client may supply these when using a 3-legged oauth token for submitting a WorkItem. |
| 3               | Status - `enum:string`                                       | 3.2.1 | url -`string` Url value                                      |
| 4               | StatusDetails - `object`                                     | 3.2.2 | signature -`string`  The signature calculated for Url.       |
| 4.1             | Report -`string: URL`                                        | 4     | limitProcessingTimeSec - `int` Max duration of processing in seconds per workitem (includes download and upload time). |
| 5               | Version - `int` should always be 1                           | 5     | n/a                                                          |
| 6               | Refer- Attributes Set Automatically by Server                | 6     | Refer- Attributes Set Automatically by Server                |

#### Attributes Set Automatically

​	This table is only for only theoretical difference . No Action is required for migration from v2 to v3, 

| Attributes | V2                                                           | V3                      |
| ---------- | ------------------------------------------------------------ | ----------------------- |
|            | AvailabilityZone                                             | status                  |
|            | TimeQueued                                                   | progress                |
|            |                                                              | stats                   |
|            | TimeInputTransferStarted                                     | reportUrl               |
|            | TimeScriptStarted                                            | timeQueued              |
|            | TimeScriptEnded                                              | timeDownloadStarted     |
|            | TimeOutputTransferEnded                                      | timeInstructionsStarted |
|            | BytesTranferredIn                                            | timeInstructionsEnded   |
|            | BytesTranferredOut                                           | timeUploadEnde          |
|            | Timestamp                                                    | timeFinishe             |
|            |                                                              | bytesDownloaded         |
|            |                                                              | bytesUploaded           |
|            | Id - `string`<br/>The value is generated by the API and is a GUID | id -`string`            |

#### Example - Post WorkItem

V2

```
curl -v 'https://developer.api.autodesk.com/autocad.io/us-east/v2/WorkItems'
  -X 'POST'
  -H 'Content-Type: application/json'
  -H 'Authorization: Bearer Jt43z2DJnsYuaAxI4R2iT84b3UPy'
  -d '
    {
      "Arguments": {
        "InputArguments": [{
          "Resource": "SIGNED_URL_TO_INPUT_FILE",
          "Name": "HostDwg",
          "StorageProvider": "Generic"
        }],
        "OutputArguments": [{
          "Name": "Result",
          "Resource": "SIGNED_URL_TO_RESULT",
          "StorageProvider": "Generic",
          "HttpVerb": "PUT"
        }]
      },
      "ActivityId": "ListLayersActivity",
      "Id": ""
    }'
```

V3

```
curl -X POST \
  https://developer.api.autodesk.com/da/us-east/v3/workitems \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -d '{
          "activityId": "YOUR_APP_NICKNAME.ListLayersActivity+my_current_version",
          "arguments": {
                  "InputDwg": {
                          "url": "SIGNED_URL_TO_INPUT_FILE",
                          "verb": "get"
                  },
                  "result": {
                          "url": "SIGNED_URL_TO_RESULT",
                          "verb": "put"
                  }
          }
    }'
```

### Get Workitem

Check the status of your workitem

| GET                | V2                         | V3                      |
| ------------------ | -------------------------- | ----------------------- |
| Get WorkItems      | {baseUrl}/WorkItems        | n/a                     |
| Get WorkItem by Id | {baseUrl}/WorkItems(‘:id’) | {baseurl}/workitems/:id |

#### Example  -Get WorkItem

V2

```
curl -v "https://developer.api.autodesk.com/autocad.io/us-east/v2/WorkItems('id')"
  -X 'GET'
  -H 'Content-Type: application/json'
  -H 'Authorization: Bearer Ck83z2DJnsYuaAxI4R2iT84b3UPy'
```

V3

```
curl -v 'https://developer.api.autodesk.com/da/us-east/v3/workitems/:id' \
  -H 'Authorization: Bearer AuIPTf4KYLTYGVnOHQ0cuolwCW2a'
```
### Delete Workitems

Cancels a specific WorkItem.

| DELETE                | V2   | V3                      |
| --------------------- | ---- | ----------------------- |
| Delete WorkItem by Id | n/a  | {baseurl}/workitems/:id |

#### Example  - Delete WorkItem

V3

```
curl -v 'https://developer.api.autodesk.com/da/us-east/v3/workitems/:id' \
  -X 'DELETE' \
  -H 'Authorization: Bearer AuIPTf4KYLTYGVnOHQ0cuolwCW2a'
```