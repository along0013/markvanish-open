# markvanish-open

Open, reusable material around **browser-local image cleanup** — removing small watermarks, logos, text and date stamps from images **without uploading the image anywhere**.

The live tool lives at **https://markvanish.com/** (free, no account, runs entirely in the browser).

This repository is not the product. It is the reference material behind it: a format-support
table, a privacy checklist for evaluating "local" claims, and a minimal standalone inpainting
demo you can read in one sitting.

## What is in here

| Path | What it is |
|:--|:--|
| `data/supported-image-formats.csv` | Input/output format support per page of the live tool, with the source page recorded for every row |
| `docs/privacy-checklist-local-image-tools.md` | A checklist for verifying that an image tool really processes locally instead of uploading |
| `tools/local-inpainting-demo.html` | A single-file, dependency-free demo of region-filling from neighbouring pixels using the Canvas API |

## Why local

An image can be personal, confidential, or simply not yours to send to a third party.
If the editing happens in the browser, the site never receives the file. That is the whole
point of this approach, and the checklist in `docs/` is how you verify it rather than take
it on faith.

## Responsible use

Only clean images you own or have permission to edit. Removing a watermark does not grant
any right to the underlying image.

## License

MIT. See `LICENSE`.
