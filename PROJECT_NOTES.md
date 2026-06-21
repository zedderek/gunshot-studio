# GUNSHOT.STUDIO Project Notes

## Working style

- Explain implementation and deployment decisions in beginner-friendly language.
- Treat Tarik as an apprentice: define unfamiliar terms and do not skip operational steps.
- Prefer reversible, low-cost changes.

## Current infrastructure

- Domain: `gunshot.studio`
- Website host: Netlify
- DNS/account: Cloudflare
- Current site: static HTML/CSS/JavaScript
- Music: SoundCloud widget API

## Content architecture direction

Do not redeploy the entire Netlify site for every daily image/video upload.

Target architecture:

1. Netlify hosts the relatively stable website code.
2. Cloudflare R2 stores the growing image/media library.
3. A small `archive.json` manifest describes titles, media URLs, dates, and types.
4. The website loads that manifest dynamically.
5. A private upload page, protected with Cloudflare Access, uploads files and updates the manifest.
6. Cloudflare Images can create optimized image sizes from R2 originals.
7. Use YouTube/Vimeo embeds initially for video, or Cloudflare Stream when paid adaptive video hosting is justified.

## Current local image workflow

- Put files in `assets/archive/`.
- Add each file to `ARCHIVE_IMAGES` in `index.html`.
- See `assets/archive/README.txt`.

This local workflow is temporary and suitable while the archive is small.
