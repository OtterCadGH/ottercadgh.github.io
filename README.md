# William Otterson - portfolio site

Plain HTML and CSS, no build step, no framework. Light theme only (locked). The only JavaScript on the site is the vendored 3D viewer on the UT Tower page (`assets/js/model-viewer.min.js`, Google's model-viewer, no CDN) and the YouTube embed on the nternet-Link page. Fonts are Inter and JetBrains Mono from Google Fonts, with system fallbacks if offline. Open `index.html` in a browser to preview.

Page structure follows the MIT MechE CommKit portfolio guidance: outcome first, an at-a-glance strip (outcome / role / constraints / skills), visuals carrying most of the page with captions doing the explaining, results, then a collapsible "Technical details" block for the reader who wants it.

## Files

```
index.html                         home: intro, project list, about, experience, contact
style.css                          all styling
projects/connector-cycler.html
projects/press-fixture.html
projects/ti-nspire-internet-link.html
projects/overdose-response-device.html
projects/ut-tower-ornament.html
projects/rc-car-chassis.html
projects/windmill-generator.html
assets/WilliamOtterson_Resume.pdf  = the General variant from Resume_WIP/02_Formatted. RULE: whenever the General resume is rebuilt, copy the new PDF here under this exact name and push.
assets/img/                        photos (see CONTENT_TODO.md for the still-empty slots)
assets/video/                      press-fixture demo (mp4 + poster); windmill demo goes here
assets/models/                     ut-tower.glb (viewer) and ut-tower.stl (download)
assets/js/                         model-viewer.min.js (3D viewer, vendored)
assets/docs/                       ME 140L assignment PDF
```

## Previewing locally

Double-clicking `index.html` works for every page except the 3D viewer on the UT Tower page: browsers block model loading from `file://`. To preview that page, serve the folder over HTTP: in VS Code use the Live Server extension (right-click `index.html` > Open with Live Server), or run `python -m http.server 8000` in the folder and open `http://localhost:8000`. On GitHub Pages it works with no extra steps.

## Hosting on GitHub Pages (free)

The site will live at `https://ottercadgh.github.io` and take about ten minutes.

1. On GitHub, create a new **public** repository named exactly `ottercadgh.github.io` (all lowercase). The name is what makes it your user site. Do not add a README or license during creation.
2. Upload the contents of this folder to the repo root. Either drag the files into the GitHub web UI ("Add file" > "Upload files", you can drag the whole folder tree), or from a terminal:
   ```
   cd portfolio
   git init
   git add .
   git commit -m "Portfolio site"
   git branch -M main
   git remote add origin https://github.com/OtterCadGH/ottercadgh.github.io.git
   git push -u origin main
   ```
3. In the repo, go to **Settings > Pages**. Under "Build and deployment", Source = "Deploy from a branch", Branch = `main`, folder = `/ (root)`. Save.
4. Wait a minute or two, then open `https://ottercadgh.github.io`. Every later push to `main` redeploys automatically.

`index.html` must sit at the repo root (not inside a subfolder) for the URL above to work.

### Optional: custom domain later

If you buy a domain (for example `williamotterson.com`, roughly $10-12 a year at Cloudflare or Namecheap):

1. Settings > Pages > Custom domain: enter the domain and save. GitHub creates a `CNAME` file in the repo.
2. At your registrar, add DNS records: four `A` records for the apex pointing to `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`, and a `CNAME` for `www` pointing to `ottercadgh.github.io`.
3. Tick "Enforce HTTPS" once the check passes (can take up to a day).

All links inside the site are relative, so nothing changes when the domain does.

## Putting it on LinkedIn

Three places, in order of visibility:

1. **Contact info > Website.** Edit your intro section > Contact info > Add website > paste the URL, type "Portfolio". This is the one recruiters look for.
2. **Featured section.** Add to profile > Recommended > Add featured > Add a link. Paste the site URL and give it the title "Engineering portfolio". LinkedIn pulls a preview card. You can also feature individual project pages (the TI Nspire page is the best candidate for a second card).
3. **Headline or About.** Optionally end the About section with "Portfolio: ottercadgh.github.io". Keep the headline itself for the role/school line.

On the resume, add the URL to the header line next to LinkedIn and GitHub. It fits the existing `linkedin.com/in/williamwotterson | github.com/OtterCadGH` pattern.

## Adding photos

Each photo slot is a `<div class="slot">` (project pages) or `<div class="img">` (home cards) containing a line-art SVG stand-in, a caption span naming the expected file, and an HTML comment with the ready-made `<img>` tag. To swap in a photo:

1. Save the image into `assets/img/` with the filename shown in the placeholder. JPG for photos, PNG for screenshots. Resize to about 1600 px on the long edge (anything bigger is wasted).
2. Uncomment the `<img ...>` line and delete the `<svg ...>...</svg>` stand-in and the `<span class="cap">` line in that slot. The image fills the slot (object-fit: cover), so crop roughly to the slot's aspect ratio (4:3 for hero and gallery slots, 2.1:1 for the wide project-page hero, 16:10 for home cards).
3. Rewrite the `alt` text if the photo shows something different from what the comment expects.

## Editing content

Everything is plain HTML. Each project page has the same sections: eyebrow, title, lede, `.glance` strip, a hero figure, `.split` sections (visual beside short text), optional `.gallery`, `.results` callouts, a `<details class="tech">` block with the spec table, and prev/next links. Copy any project page to add a new one, then add it to the list in `index.html`.

Style rules the site follows, so it stays consistent: no em or en dashes (hyphens or commas only), no emoji, one accent color, numbers only where they are defensible.
