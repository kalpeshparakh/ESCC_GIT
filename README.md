
## API Reference
```json
   #f03c15 test
```
## Getting Started
```
--------------------Initialize Azure-----------------

var storage = StorageServiceProvider.GetProvider(Provider.AZURE);

Settings.AzureSettings.ConnectionString = "{storageConnectionString}";
Settings.AzureSettings.ContainerName = "{container name}";
Settings.AzureSettings.Lifetime = {time in seconds}; // in seconds

-----------------------------------------------------

--------------------Initialize AWS-------------------

Settings.AWSSettings.AccessKey = "{access key}";
Settings.AWSSettings.SecretKey = "{secret key}";
Settings.AWSSettings.Endpoint = "{endpoint}";
Settings.AWSSettings.Ssl = true;
Settings.AWSSettings.Region = AwsRegion.EUWest3;
Settings.AWSSettings.Bucket = "{bucket name}";

-----------------------------------------------------
-- Create
await storage.CreateAsync(requests[0], token)

-- Create Multiple blobs
await storage.CreateMultipleAsync(requests, token);

-- Delete Blob by Path
var deleteres = await storage.DeleteAsync("Test0.pdf", token);

-- If Blob Exisits
var exists = await storage.ExistsAsync("Test1.pdf", token);

-- Get Blob as Stream
var blobresponseStream = await storage.GetBlobAsync("Test1.pdf", token);

-- Get List of blobs
var blobresponse = await storage.GetBlobsFromContainerAsync(token);

-- Get Blob in bytes
var bytes = await storage.GetBytesAsync("Test1.pdf", token);

-- Copy Blob
await storage.CopyFileAsync(new("privatedocuments", "Test1.pdf", "privatedocsnew",
"Testing11.pdf"), token); 

-- Get secured uri
var uri = storage.GetUri("Test1.pdf", token);
```

#### Create a Blob

```
  CreateAsync
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `createBlobRequest` | `CreateBlobRequest` | **Required**. C# Record with (Stream Content, string ContentType, string BlobName) |
| `token` | `CancellationToken` | **Required**. Cancellation token |

#### Create list of blobs

```
CreateMultipleAsync
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `createBlobRequests`      | `List<CreateBlobRequest>` | **Required**. Set of C# Records with (Stream Content, string ContentType, string BlobName) |
| `token` | `CancellationToken` | **Required**. Cancellation token |

#### Delete Blob
```
DeleteAsync
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `blobName`      | `string` | **Required**. Path of the blob |
| `token` | `CancellationToken` | **Required**. Cancellation token |

#### Bolb Exists
```
ExistsAsync
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `blobName`      | `string` | **Required**. Path of the blob  |
| `token` | `CancellationToken` | **Required**. Cancellation token |


#### Get Blob from storage
```
GetBlobAsync
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `blobName`      | `string` | **Required**. Path of the blob  |
| `token` | `CancellationToken` | **Required**. Cancellation token|

#### Get list of Blobs from storage
```
GetBlobsFromContainerAsync
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `token` | `CancellationToken` | **Required**. Cancellation token|

#### Get bytes of blob from storage
```
GetBytesAsync
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `blobName`      | `string` | **Required**. Path of the blob  |
| `token` | `CancellationToken` | **Required**. Cancellation token|


#### Get uri of the blob
```
GetUri
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `blobName`      | `string` | **Required**. Path of the blob  |
| `token` | `CancellationToken` | **Required**. Cancellation token|

#### Copy blob
```
CopyFileAsync
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `copyBlobRequest`      | `CopyBlobRequest` | **Required**.  C# Record with CopyBlobRequest(string Source, string SourceBlobName, string Destination, string DestinationBlobName) |
| `token` | `CancellationToken` | **Required**. Cancellation token|

#### Data Transfer Objects

```
  CreateBlobRequest
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Content` | `Stream` | **Required**. Content of Blob in form of System.IO.Stream |
| `SourceBlobName` | `Stream` | **Required**. Path of blob |
| `ContentType` | `string` | **Required**. Content type of blob |
| `BlobName` | `string` | **Required**. Path of blob |

```
  BlobResponse
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Name` | `string` | **Required**. Path of Blob |
| `Content` | `Stream` | **Required**. Content of Blob in form of System.IO.Stream |


```
  CopyBlobRequest
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Source` | `string` | **Required**. Source container |
| `SourceBlobName` | `Stream` | **Required**. Path of blob |
| `Destination` | `string` | **Required**. Destination container |
| `DestinationBlobName` | `Stream` | **Required**. Destination Path of blob |

