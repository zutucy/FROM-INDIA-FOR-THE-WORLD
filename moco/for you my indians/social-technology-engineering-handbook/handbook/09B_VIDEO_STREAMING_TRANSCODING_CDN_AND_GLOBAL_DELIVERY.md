# 09B — Video Streaming, Transcoding, CDN and Global Delivery

## 1. Download vs streaming

A simple download transfers a file for local storage or later playback. Streaming delivers media progressively so playback can begin before the entire asset arrives. Adaptive bitrate streaming selects among encoded renditions as network conditions and device capability change.

A platform may offer progressive MP4 for simple use cases and HLS or MPEG-DASH for adaptive streaming. Choice depends on device ecosystem, latency goals, DRM/licensing requirements and infrastructure.

## 2. Transcoding

A source video can be encoded using many codecs, profiles, resolutions, frame rates and bitrates. Not every device/network supports every format. A transcoding pipeline creates compatible renditions, for example 1080p, 720p, 480p and 360p, plus thumbnails and manifests. These are examples, not fixed requirements.

A media probe stage identifies streams, duration, dimensions, codec and metadata. Apply input limits: maximum duration, dimensions, frame rate, file size and allowed codecs. Limit processing time to prevent resource exhaustion.

## 3. Adaptive bitrate streaming

In HLS or DASH, the player reads a manifest describing available variants and requests small media segments. It can move to a lower bitrate when network capacity drops and a higher one when conditions improve. Segment duration, keyframe alignment, codec support and player buffer logic affect startup delay and switching quality.

A simplified flow:

`upload → probe → transcode variants → package segments/manifests → store → CDN → player selects rendition`

The player also reports playback events such as start, stall, quality switch and completion. Instrumentation should avoid collecting more user-level data than needed.

## 4. Video quality metrics

Useful measurements:

- time to first frame;
- startup failure rate;
- rebuffering ratio and stall count;
- average delivered bitrate/resolution;
- playback error rate;
- completion rate, interpreted carefully;
- live-stream glass-to-glass latency where applicable.

Measure by region, device, app version, ISP/network class and content encoding. A global average can hide a severe regional issue.

## 5. CDN fundamentals

A Content Delivery Network uses geographically distributed points of presence and caching to serve content near users. A request may be a cache hit or miss. On a miss, the CDN fetches from an origin or upstream cache. Cache-control headers, cache keys, origin shielding, stale serving and invalidation affect performance and cost.

For immutable versioned assets, long cache lifetimes are useful. For mutable or private content, caching needs careful design. Purge operations can be expensive and inconsistent across providers; versioned paths often simplify updates.

## 6. Live streaming is a different system

Live video has tighter latency requirements and a continuous ingest pipeline. It may include contribution ingest, transcoding, packaging, distribution, playback, chat, moderation and recording. Very low latency can require different protocols and buffering trade-offs. Live chat and live video have distinct moderation and incident risks.

Build live streaming only after VOD upload, encoding, playback and safety processes are stable. Live systems need stream keys, key rotation, permission checks, abuse controls and a way to stop a harmful broadcast quickly.

## 7. DRM and content rights

DRM is not a replacement for copyright licensing. If content owners require playback protection, evaluate supported DRM systems and device compatibility. Also implement rights-holder workflows, territorial restrictions when licensed, takedowns and repeat-infringer procedures. Never promise that technical controls can prevent all screen capture or copying.

## 8. Cost model

Video cost commonly includes:

- source and rendition storage;
- transcoding compute;
- CDN delivery/egress;
- origin requests;
- manifest/segment requests;
- thumbnail generation;
- retention, backups and replication;
- moderation review and copyright operations.

Estimate by minutes uploaded, average source bitrate, number of renditions, viewing minutes, delivery bitrate and number of regions. Playback minutes often drive more delivery cost than the upload itself.

## 9. Practical lab

Use a test video you own. Run `ffprobe` to inspect it; transcode two renditions with FFmpeg; package HLS; serve locally; use a supported player; throttle network bandwidth; observe rendition switching; inspect logs for startup and stall events. Do not test with copyrighted content unless you have rights.

## Further reading

- Apple HTTP Live Streaming resources: https://developer.apple.com/streaming/
- MPEG-DASH overview: https://www.mpeg.org/standards/MPEG-DASH/
- FFmpeg documentation: https://ffmpeg.org/documentation.html
- Cloudflare CDN docs: https://developers.cloudflare.com/cache/
- AWS CloudFront docs: https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html
