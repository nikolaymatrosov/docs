# copy method

Creates a copy of an object stored in [!KEYREF objstorage-name]. Objects up to 5 GB in size can be copied with a single `copy` operation. If the object is greater than 5 GB, use the [copyPart](../multipart/copypart.md) operation.

To specify the copy source, use the `x-amz-copy-source` header. The copy request must not pass any data other than headers.

> [!NOTE]
>
> [!KEYREF objstorage-name] does not lock an object for writing and can simultaneously accept multiple requests that copy objects to the same resulting object. After all the requests are completed, the resulting object is the one whose copy operation was run last.

The object metadata is copied along with the object. If necessary, you can change the metadata by explicitly setting the appropriate headers.

You can also use headers to:

- Change an object's storage class.
- Add conditions for copying an object.

The user must have permission to read the source object and write data to the resulting bucket.

## Request {#request}

```
PUT /{bucket}/{key} HTTP/1.1
```

### Path parameters {#path-parameters}

| Parameter | Description |
| ----- | ----- |
| `bucket` | Name of the resulting bucket. |
| `key` | Key of the resulting object. ID under which the object is saved in [!KEYREF objstorage-name]. |

### Headers {#request-headers}

Required headers are listed in the table below.

| Header name | Description |
| ----- | ----- |
| `x-amz-copy-source` | The name of the bucket and the key of the object to copy, separated by the `/` character.<br/><br/>For example, `x-amz-copy-source: /source_bucket/sourceObject`. |

You should also use the necessary [common request headers](../common-request-headers.md).

Use the headers from the table below if you need to change the default behavior of the `copy` method.

| Header name | Description |
| ----- | ----- |
| `x-amz-metadata-directive` | Metadata copy mode.<br/><br/>If the header value is `COPY`, the object metadata is copied and all the `x-amz-meta-*` headers are ignored. Default behavior of the `copy` method.<br/><br/>If the header value is `REPLACE`, the object metadata is replaced with the metadata specified in the request.<br/><br/>The `x-amz-storage-class` header is not copied; add it to the request if necessary. |
| `x-amz-copy-source-if-match` | Condition for copying an object.<br/><br/>If the object's `ETag` matches the one specified in the header, the object is copied.<br/><br/>If the condition is not met, [!KEYREF objstorage-name] returns error 412.<br/><br/>Can be used with the `x-amz-copy-source-if-unmodified-since` header. |
| `x-amz-copy-source-if-none-match` | Condition for copying an object.<br/><br/>If the object's `ETag` does not match the one specified in the header, the object is copied.<br/><br/>If the condition is not met, [!KEYREF objstorage-name] returns error 412.<br/><br/>Can be used with the  `x-amz-copy-source-if-modified-since` header. |
| `x-amz-copy-source-if-unmodified-since` | Condition for copying an object.<br/><br/>The object is copied if it has not been modified since the specified time.<br/><br/>If the condition is not met, [!KEYREF objstorage-name] returns error 412.<br/><br/>Can be used with the `x-amz-copy-source-if-match` header. |
| `x-amz-copy-source-if-modified-since` | Condition for copying an object.<br/><br/>The object is copied if it has been modified since the specified time.<br/><br/>If the condition is not met, [!KEYREF objstorage-name] returns error 412.<br/><br/>Can be used with the `x-amz-copy-source-if-none-match` header. |
| `x-amz-storage-class` | Object storage class.<br/><br/>Possible values:<br/>- `STANDARD` for uploading an object to standard storage.<br/>- `COLD`, `STANDARD_IA`, and `NEARLINE` for uploading an object to cold storage.<br/><br/>If the header is omitted, the object is saved in standard storage. |
| `x-amz-meta-*` | User-defined metadata for the object.<br/><br/>All headers starting with `x-amz-meta- are considered by` [!KEYREF objstorage-name] to be user-defined. It does not process these headers, but saves them in the original form.<br/><br/>The total size of user-defined headers should not exceed 2 KB. The size of user-defined data is determined as the length of the UTF-8 encoded string. Both request names and values are included in the size.<br/><br/>If `x-amz-metadata-directive: COPY`, such headers are ignored. |

## Response {#response}

### Headers {#response-headers}

A response may contain [common response headers](../common-response-headers.md) and the headers listed in the table below.

| Header name | Description |
| ----- | ----- |
| `x-amz-storage-class` | Object storage class.<br/><br/>Possible values:<br/>- `STANDARD` for an object stored in standard storage.<br/>- `COLD` for an object stored in cold storage. |

### Response codes {#response-codes}

For a list of possible responses, see [[!TITLE]](../response-codes.md).

### Data schema {#response-scheme}

```
<CopyObjectResult>
   <LastModified>2019-02-15T14:32:00</LastModified>
   <ETag>"9bgh7535f2734ec974343yuc93985328"</ETag>
</CopyObjectResult>
```

| Element | Description |
| ----- | ----- |
| `CopyObjectResult` | Contains response elements.<br/><br/>Path: `/CopyObjectResult`. |
| `ETag` | `ETag` of the resulting object. Because metadata is not taken into account when calculating the `ETag`, the `ETag` of the source and resulting objects must match.<br/><br/>Path: `/CopyObjectResult/ETag`. |
| `LastModified` | Date when the object was last modified.<br/><br/>Path: `/CopyObjectResult/LastModified`. |

