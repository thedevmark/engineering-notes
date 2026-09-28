# 4K60 Native Ingest: why iPhone uploads looked better

**Date:** 2026-09-28

**Status:** engineering field report; controlled platform comparison pending

## Abstract

Mark reports testing about 40 vertical short-form videos. Across that work, genuine 4K/60 fps exports uploaded through an iPhone produced more consistently good-looking posts on YouTube, TikTok, Instagram, Threads, Facebook, and X than his other upload paths. A narrower TikTok desktop investigation supplied a measurable failure: two downloaded test streams were 576 × 1024 at 30 fps, despite a 60 fps source and an active browser upload hook. The roughly 40-video experience is substantial field testing, while the two streams are the retained frame-rate measurements. Together they justify testing and preserving the native phone path. They do not establish that iPhone uploads always deliver 4K/60, that every desktop upload loses frames, or which stage caused the difference.

This paper separates the source file, phone or browser preparation, server processing, and viewer playback. It explains why local iPhone processing is a plausible mechanism, what the public documentation actually supports, and the experiment needed to locate the quality loss.

## 1. The failure was downstream of the export label

A finished file can be 2160 × 3840 at 59.94 or 60 progressive frames per second without viewers ever receiving that representation. The upload and playback pipeline has distinct boundaries:

| Stage | Evidence to capture | What it proves |
| --- | --- | --- |
| Source export | SHA-256, dimensions, frame timestamps, codec, bitrate, color metadata, duration | What was available before upload. |
| Transfer and selection | Exact selected file and, if possible, its bytes after transfer | Whether the intended source entered the composer. |
| App preparation | Any trim, render, export, or replacement file | Whether the client changed the media. |
| Platform processing | Available encoded renditions and processing completion | What the service prepared. |
| Viewer playback | Rendition fetched on a specified client and connection; displayed frame cadence | What that viewer received. |

The source's `60 fps` metadata does not prove 60 fps playback. A completed upload does not prove it either. An extension status icon can establish that a local hook is active; it cannot establish what TikTok eventually encodes or serves. Conversely, an early low-resolution preview is not conclusive: [YouTube says lower-quality versions are available first while higher-resolution processing continues](https://support.google.com/youtube/answer/71674?hl=en-GB).

The word *throttling* describes the experience of lower quality, but the evidence here does not identify an account-level penalty or deliberate reach suppression. The measurable questions are resizing, re-encoding, frame-rate conversion, processing delay, and rendition selection.

## 2. What we observed

| Observation | Strength | Limit |
| --- | --- | --- |
| Mark reports testing about 40 videos and found iPhone uploads of genuine 4K/60 vertical exports to be the most consistently high-quality path in his own use of YouTube, TikTok, Instagram, Threads, Facebook, and X. | Roughly 40 videos of first-person field testing. | The per-platform counts, matched upload pairs, and a same-file, same-account, same-age playback matrix are not archived here. |
| Two TikTok streams downloaded during the desktop investigation measured 576 × 1024 at 30 fps. | Measured properties recorded in the local `60fps-upload-helper` README. | Two streams are a small sample; the fetched rendition can depend on device, network, account, and processing state. |
| The TikTok browser hook was active but did not demonstrate a delivered 60 fps post. | Local hook tests and the two stream measurements. | No verified live 60 fps result from that hook. |
| The separate Video Drop project has a documented OneDrive → iOS share sheet → native app path, with a YouTube composer preparation runner. | Repository source and runbook. | An end-to-end published post and playback-quality receipt are not established by those source checks. |

The two-stream TikTok measurement is evidence about those particular streams, not the size of the overall video testing or every rendition TikTok might have stored. The other five platforms have no comparable measured output retained in this report. It would be inaccurate to turn Mark's roughly 40-video visual finding into six measured 4K/60 delivery claims.

## 3. What the platform documentation says

[YouTube's upload guidance](https://support.google.com/youtube/answer/1722171?hl=en) recommends encoding at the frame rate recorded, lists 60 fps as a common rate, and provides separate suggested bitrates for high-frame-rate 4K. That supports preparing a genuine 60 fps source. It does not promise a specific served frame rate. [YouTube's processing guidance](https://support.google.com/youtube/answer/71674?hl=en-GB) says 4K and 60 fps can take longer to process, so comparisons must wait for processing to settle.

[TikTok's Content Posting API media guide](https://developers.tiktok.com/docs/en/content-posting-api-media-transfer-guide) allows input up to 60 fps. Input acceptance is a different claim from delivered playback, and that API guide does not document the desktop website's or iPhone app's complete processing path.

Apple supplies [AVFoundation media export](https://developer.apple.com/documentation/avfoundation/avassetexportsession?language=objc), [VideoToolbox hardware-assisted video encoding and decoding](https://developer.apple.com/documentation/videotoolbox?language=objc), and [iOS share-sheet transfer between apps](https://developer.apple.com/documentation/uikit/collaborating-and-sharing-copies-of-your-data?changes=_5). These make on-phone inspection, export, and encoding technically possible and efficient. They do **not** reveal whether a specific social app uses those APIs for a given upload, which settings it selects, or whether a server later changes the result.

## 4. The iPhone processing hypothesis

The strongest working hypothesis is that the **upload path** matters. A browser, an official API client, and a native iPhone app may submit different bytes or metadata, may apply different local edits, and may trigger different server processing. The iPhone has local media frameworks and hardware encoding support, so a native app can prepare video on the device before upload. In Video Drop's Instagram route, the documented OneDrive → Edits → Instagram path includes an explicit on-phone export where resolution, frame rate, and color mode must be inspected. The YouTube path selects the file through OneDrive and the native Shorts composer. Those are distinct workflows and should not be treated as one hidden algorithm.

We have not captured the social apps' outbound media bytes or instrumented their internal encoders. It is also possible that the phone path simply helps the operator select the intended high-quality source and avoid an accidental intermediate export. OneDrive, a share-sheet handoff, an app editor, or platform processing could still create a lower-quality derivative. The observed result does not isolate which stage is responsible.

## 5. Practical export rule

When the footage and edit genuinely contain the detail, use a **2160 × 3840 (9:16), 59.94 or 60 fps progressive** vertical export. Keep the original temporal cadence. Upscaling a lower-resolution image or inventing frames only changes the file label; it does not recover missing detail. For a standard SDR workflow, tag the export consistently with [YouTube's BT.709 guidance](https://support.google.com/youtube/answer/1722171?hl=en). Verify the selected phone file, account, and final public text, then judge the published result after processing on a separate playback device.

This is an engineering recommendation for preparing and checking the source. It is not a 4K/60 delivery guarantee. The separate Video Drop tool is still in migration: its local editor and phone preparation work do not themselves prove unattended uploads or platform receipts.

## 6. Experiment that would settle the claim

1. Build one test clip from genuine 2160 × 3840, 59.94/60 progressive source frames. Include motion, fine texture, small text, and a frame counter. Record source hash, dimensions, actual frame timestamps, codec, bitrate, color tags, duration, and file size.
2. Submit the same source through desktop and native iPhone paths to the same platform account and visibility, using matching post settings and separate posts. Record post IDs and upload times.
3. Record every observable intermediate export and client setting. Mark app-internal or encrypted upload stages as unknown instead of inferring their behavior.
4. Wait for processing to settle. On at least two playback devices and connections, record the selected rendition, encoded dimensions and frame rate, bitrate, codec, and displayed frame cadence. Retain the stream and measurement command where permitted.
5. Compare like with like: same service, account, post age, playback client, and rendition choice. Repeat with several clips across several days.

A reproducible difference in served renditions would establish a path-dependent result. Additional instrumentation would still be needed to assign the cause to on-phone preparation, platform processing, or viewer-side rendition selection.

## 7. Evidence boundary

This report draws on Mark's reported testing of about 40 videos, the September 2026 TikTok desktop investigation, Video Drop's phone runbook, and the primary documentation linked above. The per-video test log and platform breakdown are not included here. The local helper README recorded the two TikTok stream properties, but its raw test media and network captures are not included here. Platform behavior may change. The conclusion supported today is narrower than a universal platform rule: **across about 40 videos, the iPhone path worked better for this operator; two measured desktop TikTok streams were 30 fps.**
