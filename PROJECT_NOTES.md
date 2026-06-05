# Shanta & Lauren — Anniversary Website

## Overview
A scrapbook-style anniversary website for Shanta (builder) and Lauren (recipient).
Single-file site: everything lives in `index.html`. Images sit in the same directory.

**Live URL:** https://shantarakshit.github.io/anniversary
**Repo:** https://github.com/shantarakshit/anniversary
**Anniversary date:** July 25, 2025 (set in JS: `const START = new Date('2025-07-25')`)

---

## Design
- **Style:** Scrapbook / polaroid — elegant but cute
- **Colors:** Pink (`#E8A0B4`, `#C97A96`) + Sage green (`#A8C5A0`, `#7A9E72`) on cream (`#FFF8F2`)
- **Fonts:** Dancing Script (handwritten headings), Playfair Display (italic body), Lato (UI)
- **Features:**
  - Full-screen hero (Ken Burns zoom) using `PXL_20250717_004553503.jpg` ("Howdy Babe" photo)
  - Live days-together counter calculated from anniversary date
  - Vertical timeline with alternating left/right polaroid cards, grouped by season
  - Scroll-triggered fade/slide animations (IntersectionObserver)
  - Click-to-expand photo lightbox (Esc or click outside to close)
  - Floating pink/green petals background animation
  - ♪ play/pause button (bottom-right) — plays YouTube Music playlist in background via YouTube IFrame API

---

## Music
- **Button:** Fixed ♪ bottom-right corner. Click to play, click again to pause. No popup.
- **Player:** Hidden YouTube IFrame embed (`div#yt-el` off-screen)
- **Playlist URL:** https://music.youtube.com/watch?v=6TIZQO9m9nQ&list=QPJD-tutyqw2o9h_xjyX5f-63waVLv4Worj
- **Artists:** Noah Kahan, Tyler Childers, Ben Howard
- **Note:** YouTube IFrame API requires HTTP/HTTPS — won't work opening `index.html` directly as a file. Use `python3 -m http.server 8765` to test locally or use the GitHub Pages URL.
- **Note:** The `QP` prefix playlist ID is YouTube Music-specific. The API will always play the first video; full playlist cycling may vary. A `PL`-prefix YouTube playlist ID would be more reliable if needed.

---

## Photos (16 total, sorted by EXIF date)

| File | Date | Caption | Season |
|------|------|---------|--------|
| PXL_20250704_031107228.jpg | Jul 3, 2025 | Summer nights and live music | Summer 2025 |
| PXL_20250712_031539098.jpg | Jul 11, 2025 | Lit up in blue light & your smile | Summer 2025 |
| PXL_20250717_004553503.jpg | Jul 16, 2025 | Howdy, babe. Always. *(also hero image)* | Summer 2025 |
| PXL_20251004_003019287.TS-000.jpg | Oct 3, 2025 | Golden hour at the lake | Fall 2025 |
| PXL_20251023_232052410.jpg | Oct 23, 2025 | Stolen kisses in the cornfield | Fall 2025 |
| PXL_20251130_024941634.jpg | Nov 29, 2025 | Carousel rides & the best view | Fall 2025 |
| PXL_20251226_042028106.jpg | Dec 25, 2025 | Matching sweaters, matching hearts | Winter 2025 |
| PXL_20260216_050144464.jpg | Feb 15, 2026 | Every journey is better together | Winter 2026 |
| PXL_20260305_233124731.jpg | Mar 5, 2026 | Just us and an endless blue sky | Spring 2026 |
| PXL_20260319_005421177.jpg | Mar 18, 2026 | My favorite little moment | Spring 2026 |
| PXL_20260328_073842317.jpg | Mar 28, 2026 | Dessert for two & zero dignity | Spring 2026 |
| PXL_20260401_045852271.jpg | Mar 31, 2026 | Gym dates & matching energy | Spring 2026 |
| PXL_20260410_224127603.jpg | Apr 10, 2026 | All dressed up, nowhere I'd rather be | Spring 2026 |
| PXL_20260411_023439526.jpg | Apr 10, 2026 | Date night — you light up every room | Spring 2026 |
| PXL_20260423_234447250.jpg | Apr 23, 2026 | Cheers to us, always | Spring 2026 |
| PXL_20260527_174719823.jpg | May 27, 2026 | Every adventure is better with you | Spring 2026 |

---

## How to add new photos
1. Drop the new `.jpg` files into `/Users/buffries/PycharmProjects/HelloWorld/`
2. Check their EXIF date with:
   ```bash
   python3 -c "from PIL import Image; from PIL.ExifTags import TAGS; img=Image.open('FILENAME.jpg'); [print(TAGS.get(k,k),v) for k,v in img._getexif().items() if TAGS.get(k,k)=='DateTimeOriginal']"
   ```
3. In `index.html`, find the right season section and add a new `.row` block — copy an existing one and update the filename, date, and caption
4. If the photo falls in a new season, add a `<div class="season">` divider before it
5. Alternate `.row` and `.row right` for left/right placement

## How to update a caption
Search for the current caption text in `index.html` — it appears twice per card: in `data-cap="..."` (lightbox) and in `<span class="card-caption">`. Update both.

## How to change the hero image
Search for `PXL_20250717_004553503.jpg` — it appears in 2 places: the CSS background in `#hero-bg` and the JS preload probe. Replace both with the new filename.

---

## Deployment
- **Repo:** git@github.com:shantarakshit/anniversary.git (SSH)
- **Hosting:** GitHub Pages — auto-deploys from `main` branch root
- **To push updates:**
  ```bash
  git add index.html <any-new-photos.jpg>
  git commit -m "describe change"
  git push
  ```
- **SSH key** is set up on this machine (`~/.ssh/id_ed25519`) — no token needed

---

## Local preview
```bash
cd /Users/buffries/PycharmProjects/HelloWorld
python3 -m http.server 8765
# open http://localhost:8765
```
