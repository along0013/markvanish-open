# Checklist: does an image tool really process locally?

Many tools say "private" or "no upload" in their marketing. This is how to check it yourself,
in about five minutes, without trusting the claim.

## 1. Disconnect the network and retry

The decisive test.

1. Open DevTools -> Network tab.
2. Load the tool page and drop an image in.
3. Run the cleanup.

- **No request carries the image** (no `POST` with a large body, no `PUT` to a storage URL)
  -> processing is local.
- **Any request with a body roughly the size of your image** -> the file is being uploaded.

Watch for requests to analytics or ad endpoints. They are a separate privacy question and do
not by themselves mean the image left the browser, but note them.

## 2. Check the code path, not the copy

Search the page source for:

- `CanvasRenderingContext2D` operations -> local pixel work
- `createImageBitmap`, `OffscreenCanvas` -> local decode
- `fetch(`, `XMLHttpRequest`, `FormData` near the processing step -> upload

A tool can have `fetch` calls for unrelated things (version checks, telemetry). What matters
is whether any of them carries pixel data.

## 3. Check where the decode happens

HEIC and HEIF are the tell. These formats often cannot be decoded natively by the browser, so
a tool that claims to support them is either:

- using a local WebAssembly decoder (still local), or
- sending the file to a server to convert it (not local).

If the tool silently fails on HEIC in some browsers, that is consistent with genuinely local
decoding.

## 4. Check the session lifecycle

A real local tool should lose everything on refresh. Reload the page mid-edit: the image should
be gone, with no server-side draft to restore.

## 5. Things this checklist does not cover

- Whether the site logs your IP or sets cookies (it probably does; that is normal).
- Whether the tool keeps a local copy in IndexedDB after you leave.
- Legal questions about the image itself.

## Why this matters for watermark removal specifically

Watermarked images are frequently screenshots, personal photos, or client material. Sending
such a file to an unknown third party is a bigger exposure than the watermark is an
inconvenience — and in most jurisdictions removing a watermark does not grant you any right
to the image either way.

---

Reference implementation of the local approach: https://markvanish.com/
