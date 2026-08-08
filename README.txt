ALI ZAIN — PORTFOLIO WEBSITE
=============================
Static site — no build step, no dependencies, no database. Pure
HTML/CSS/JS. Works on cPanel (Apache) AND on GitHub Pages, unchanged.

HOW TO HOST — TWO OPTIONS
----------------------------
A) cPanel (paid hosting you already have)
   1. Log into cPanel > File Manager (or use FTP).
   2. Open "public_html" (your site's web root).
   3. Upload ALL files and folders from this package directly into
      public_html — index.html should sit at public_html/index.html,
      not inside a subfolder.
   4. If uploading the .zip, use cPanel's "Extract" feature, then make
      sure the extracted files land directly in public_html.
   5. Delete CNAME and .nojekyll first — those two files are only
      meaningful to GitHub Pages and are harmless either way, but
      there's no reason to upload them to cPanel.
   6. Visit your domain — the site is live immediately.

B) GitHub Pages (free) — see the full step-by-step walkthrough your
   chat conversation with Claude ended with. Short version: push this
   folder's contents to a GitHub repo, enable Pages on the main
   branch, and point your domain's DNS at GitHub using the values in
   the CNAME file (already set to www.alizain.pk).

FILES TO REPLACE / ADD
-----------------------
1. Profile photo (REQUIRED for the new About section)
   Path: assets/img/profile.webp
   Drop your photo in at this exact filename. Your 4096x4096 source is
   fine as-is — the frame is a 1:1 square with object-fit:cover, so it
   crops to fit automatically without distortion; no manual resizing
   needed. Until you add it, the frame shows a clean "aZ" placeholder
   instead of a broken image icon.

2. Resume PDF
   Path: assets/docs/Ali-Zain-Resume.pdf
   Add your actual resume PDF with this exact filename (or update the
   links in index.html and the three page files below).

3. Social preview image (optional, for link previews on WhatsApp/LinkedIn)
   Path: assets/img/og-cover.webp — a 1200x630px image works best.

4. Contact form
   Uses FormSubmit.co (free, no backend) posting to contact@alizain.pk.
   The FIRST submission after upload triggers a one-time confirmation
   email — click "Confirm" there to activate the form. Works identically
   on cPanel or GitHub Pages since it's a client-side form post.

CLEAN URLS (no .html in the address bar) — HOST-AGNOSTIC NOW
----------------------------------------------------------------
Every page loads without an extension:
  www.alizain.pk
  www.alizain.pk/experience/
  www.alizain.pk/case-studies/
  www.alizain.pk/resume/
  www.alizain.pk/contact/

This is done by giving each page its own folder with an index.html
inside (e.g. experience/index.html) — every static host, including
GitHub Pages, Apache/cPanel, Netlify and Vercel, serves a folder's
index.html automatically for a request to that folder. No rewrite
rules, no redirects, no host-specific configuration required. This
replaced the earlier .htaccess-rewrite approach, which only worked on
Apache and was the source of the "homepage needs a refresh" / "mobile
view unstyled" bug from before — that's now structurally impossible,
since asset links are root-absolute (/assets/...) and every page's
real file already sits at the URL depth the browser expects.

.htaccess is still included for when this is hosted on Apache/cPanel
(security headers, GZIP, caching, HTTPS+www enforcement) — GitHub
Pages ignores it completely since it doesn't run Apache, so it's
harmless to leave in the repo either way.

If you deployed an EARLIER build of this site to cPanel: replace the
ENTIRE public_html contents with this package, don't merge individual
files — the folder structure changed (experience.html is now
experience/index.html, etc).

ROOT / SEO / PWA FILES
-----------------------
These sit in the root next to index.html and each serve a purpose:

- .htaccess        Apache rules: forces HTTPS, forces non-www, serves
                    clean URLs (see above), sets security headers,
                    enables GZIP + browser caching, blocks directory
                    listing, points 404s to /404.html.
- robots.txt        Tells search engines everything is crawlable and points
                    them to sitemap.xml.
- sitemap.xml        Lists all 5 clean-URL pages for Google/Bing indexing.
                    Update <lastmod> whenever you make real content changes.
- site.webmanifest   Lets mobile users "Add to Home Screen" — uses the same
                    ink-navy/signal-teal brand colors and the icons below.
- security.txt        A standard (RFC 9116) file researchers check before
                    reporting a vulnerability responsibly. Included at both
                    /security.txt and the spec-correct /.well-known/security.txt.
- browserconfig.xml   Legacy Microsoft file — controls the tile color/icon
                    if someone pins the site to a Windows Start Menu (IE11 /
                    old Edge only). No effect in modern browsers, kept for
                    parity with the previous site. Uses assets/img/mstile-*.png.
- 404.html          Custom not-found page in the site's own design, wired
                    up via .htaccess.
- favicon.ico, assets/img/icon-192.png, icon-512.png, apple-touch-icon.png
                    Generated brand-mark icons (ink navy + signal teal "aZ")
                    used by the browser tab, home-screen icon, and manifest.

WHAT'S INSIDE
-------------
index.html                 Home — now with a profile photo panel in the About section
experience/index.html      Full career timeline, education & certifications
case-studies/index.html    5 case studies + focus areas
resume/index.html          Web resume + PDF download
contact/index.html         Contact details, form, FAQ
assets/css/style.css       Design system (all styling)
assets/js/main.js          Mobile nav, animated counters, diagram animation
assets/docs/                Put your resume PDF here
assets/img/                 Put profile.webp and other photos here
CNAME                       GitHub Pages custom-domain file (already set to
                            www.alizain.pk) — ignored by cPanel; delete it
                            there if you'd rather not have a stray file.
.nojekyll                   Tells GitHub Pages to skip its Jekyll build step
                            and serve files exactly as they are — needed
                            since this is a plain static site, not Jekyll.
                            Ignored by cPanel.

DESIGN
------
Theme: "Schematic" — a blueprint/network-diagram aesthetic built around
Ali's actual discipline (systems & network administration): dot-grid
background, signal-teal accent, mono command-style section labels, an
animated topology diagram in the hero, and a CCTV/biometric-style
verification frame around the profile photo (scan line + corner
brackets). A blinking terminal cursor follows each section's mono
label. Fully responsive, keyboard accessible, and respects
reduced-motion preferences throughout.

Stat blocks (hero, Experience page, Resume page) now consistently show
three matched number+label pairs — years of experience, organizations,
and core IT disciplines — center-aligned, with the number animating up
on scroll and a smaller, stable label beneath it.

Fonts (Google Fonts, loaded via CDN): Space Grotesk, Inter, JetBrains Mono.
No paid licenses, no external frameworks required.

