# The Razor: website mockup

A one-page website for **The Razor**, Henry Rodriguez's barbershop at 14799 Yonge St, Aurora, ON ([@lineupforyourlineups](https://www.instagram.com/lineupforyourlineups/)). Plain HTML, CSS and JavaScript with no build step, so it runs on GitHub Pages as-is.

Live: https://therazor.ca/ (Cloudflare Worker "the-razor", also mirrored at https://jdix22.github.io/the-razor/)

## Highlights
- **Scroll-driven haircut.** Henry's own transformation video (man bun to skin fade) plays forward as you scroll down and backward as you scroll up, inside a gold barber mirror. Captions change with each stage of the cut, and gold drips run off the mirror frame as it goes, echoing the dripping blade in his logo.
- **Phones** get the same video as a short silent loop instead of the scroll scrub, plus a sticky Call / Book bar.
- **Before/after slider** with a razor-blade handle, built from the first and last frames of that same video. Drag, swipe or use the arrow keys.
- **Book without leaving the site.** Booksy's official embed (business ID 7103) runs inline in the "Book your chair" section, and every Book button opens it in a pop-up. No API keys needed. Clients see Henry's real services, prices and open times, and confirmations come from Booksy as usual.
- **Instagram strip** that updates itself from his Behold.so feed (newest six posts), each linking to the post, plus Follow buttons.
- Services and prices (from Booksy), Gold service feature card, Meet Henry, reviews (5.0 from 204 on Booksy), hours with a live "Open now" status in Toronto time, map and directions.
- SEO basics: title, meta description, Open Graph tags and `BarberShop` structured data.

## Files
- `index.html`: the whole site
- `assets/hero-scrub.mp4`: the scroll video (21 s, keyframe every 8 frames so scrubbing stays smooth)
- `assets/hero-loop.mp4`: lighter loop for phones
- `assets/hero-poster.jpg`, `assets/hero-ending.jpg`: first and last frames
- `assets/img/`: logo, before/after pair, shop photos (from the-razor.ca and Booksy)
- `assets/ig/`: saved Instagram post images

## Editing
All of the settings live at the top of the `<script>` in `index.html`:
- `IG_POSTS`: the saved Instagram posts (post ID, type and a short description). Drop a new image into `assets/ig/<id>.jpg` and add a line.
- `IG_FEED_URL`: Henry's Behold.so JSON feed (connected 2026-10-29). Its posts are merged with `IG_POSTS`, newest first, so his new posts appear automatically. Instagram doesn't give Behold collab posts, which is why the saved ones stay in the mix.
- `IG_HIDE`: post IDs to keep off the site even if they're in the feed. Henry can also hide posts inside Behold.
- `HOURS`: opening hours used for the "Open now" badge and the highlighted day. The hours table and footer text are plain HTML just below.
- Prices: the service list in the `#menu` section. Booksy is the source of truth for what clients actually pay.
- Colours: CSS variables at the top of `<style>` (`--gold`, `--metal` and friends).

## Previewing locally
Double-clicking `index.html` works, but browsers block the video download on `file://`, so you'll see the still image instead of the scroll video. For the full effect, serve the folder (for example `npx http-server`) and open the localhost link.

## Deploying
therazor.ca and www.therazor.ca are served by a Cloudflare Worker that hosts this folder as static files (`wrangler.jsonc`; `.assetsignore` keeps the README and config private). After changing anything, run `npx wrangler deploy` from this folder. Pushing to GitHub only updates the github.io copy.

If the domain ever changes, update `og:url`, `og:image`, `canonical` and the JSON-LD urls in `<head>`.
