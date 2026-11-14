# 09A — Object Storage, Uploads, Media Pipelines and File Security

## 1. Why files need a different storage design

A relational database is good for structured records and transactions. Photos, videos, audio and large documents are usually stored in object storage or a specialised media system. The database stores metadata and a reference to the object, not usually the entire media binary.

A media record may include an ID, owner, object key, content type, byte size, dimensions, duration, checksum, visibility, processing state, creation time and retention/deletion state. Never assume a client-supplied filename or MIME type is trustworthy.

## 2. Object storage concepts

Object storage stores data as objects in buckets/containers, each with a key and metadata. It is designed for large unstructured objects and high durability, not arbitrary SQL joins. Examples include Amazon S3, Google Cloud Storage, Azure Blob Storage and Cloudflare R2.

Important concepts:

- bucket/container access policy;
- object key naming and tenant separation;
- private vs public access;
- lifecycle and archival rules;
- versioning and delete markers;
- encryption at rest;
- checksums/integrity;
- regional location and replication;
- request cost and bandwidth/egress cost;
- signed URLs and policy-based uploads.

Use random, non-guessable object keys. Do not derive public access solely from the key being hard to guess. Enforce access using bucket policy and application authorisation.

## 3. Upload patterns

### Server-proxied upload

Browser sends file to application server; server validates and forwards it to storage. Simpler control flow but consumes application bandwidth, memory/temporary disk and connection capacity.

### Direct-to-object-storage upload

Application authorises an upload and returns a short-lived signed URL or upload policy. Browser sends bytes directly to object storage. This reduces load on the application server, but the backend must still verify the completed object, size, owner, type, checksum and lifecycle.

### Multipart/resumable upload

Large uploads are split into parts or chunks. Client can retry failed parts, resume within a supported session and complete after all parts are verified. Design expiry, abort cleanup, quotas, part-size limits and abuse prevention. A client reporting “upload complete” is not proof that the object is valid.

## 4. Secure upload pipeline

A safer sequence:

1. Authenticate user and check quota/permission.
2. Create a pending media record.
3. Issue a scoped, short-expiry upload capability.
4. Upload into a quarantine or private incoming area.
5. Verify actual byte size, checksum and content signature.
6. Inspect file structure with maintained libraries and sandboxed processors.
7. Scan for malware where the threat model and file types justify it.
8. Decode/re-encode images or media in isolated workers.
9. Generate safe derivatives and thumbnails.
10. Store approved output in a delivery area.
11. Mark record ready and expose through an authorised delivery path.
12. Clean up rejected, abandoned and expired uploads.

A file extension is only a hint. Validate file signatures and parse content safely. Processors such as image decoders and FFmpeg are complex attack surfaces: keep them patched, isolate them, restrict network access, set CPU/memory/time limits and use least privilege.

## 5. Image processing

Common tasks include orientation correction, resizing, thumbnails, format conversion, metadata removal and responsive variants. EXIF metadata can reveal location/device information, so decide whether to strip or selectively retain it. Keep an original only when there is a defined need and retention policy.

Serve responsive sizes so a phone does not fetch a 20-megapixel original for a small avatar. Preserve aspect ratio and avoid repeated lossy re-encoding where possible.

## 6. Video and audio processing

A media pipeline may probe a file, validate codecs, transcode renditions, generate thumbnails, extract audio, normalise audio and create streaming manifests. Use a queue and worker pool rather than running heavy FFmpeg work inside a normal request. Track states such as `pending`, `uploading`, `queued`, `processing`, `ready`, `rejected` and `failed`.

Retries must be idempotent. A worker may crash after writing a 720p rendition but before updating the database. A retry should detect or safely replace the output and produce one valid final state.

## 7. Signed URL security

A signed URL is a temporary capability. Anyone who obtains it may be able to use it until it expires or its underlying permission changes. Keep expiry short, scope it to one object and one operation, avoid logging the full URL, use HTTPS and do not place it in public analytics. A signed upload URL does not mean the uploaded file is safe or approved.

## 8. CDN and private media

A CDN caches and serves objects closer to users. Public assets can often be cached aggressively with versioned URLs. Private media needs authenticated origin access, signed delivery URLs/cookies or another access-control design. Cache keys and cache policies must account for identity/visibility. A misconfigured shared cache can leak private media between users.

## 9. Cost planning

Estimate storage as `objects × average size × retained copies/versions`. Estimate delivery as `views × average transferred bytes`. Include thumbnails, transcoded renditions, retries, abandoned uploads, backup copies, request fees and egress. Different cloud providers price requests, storage classes and network egress differently; use current provider calculators and actual measurements.

## 10. Practical lab

Build a private image upload flow using a local S3-compatible service or a cloud test bucket. Use signed URLs, verify ownership in the API, reject unsupported files, create a thumbnail in a worker, and test that another account cannot retrieve the private original.

## Further reading

- Amazon S3 User Guide: https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html
- Google Cloud Storage docs: https://cloud.google.com/storage/docs
- Azure Blob Storage docs: https://learn.microsoft.com/en-us/azure/storage/blobs/
- Cloudflare R2 docs: https://developers.cloudflare.com/r2/
- OWASP File Upload Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html
