# Ambient Night Light

A silent ambience page for a projector: starfield, fireplace and campfire modes, with adjustable brightness and speed, plus a 30/60/90 minute sleep timer that fades the screen to black. It makes no sound of its own, so you can play music over it.

**Live:** https://tszyilin.github.io/projector_background/

## Modes

Nine palettes, three of which add animation on top of the drifting colour wash:

| Palette | What you get |
| --- | --- |
| Starfield | Slow twinkle plus the occasional shooting star |
| Fireplace | A full-width bed of embers with soft, swaying flames |
| Campfire Sky | Both at once — stars above, a compact fire below |
| Amber, Deep Sea, Aurora, Lavender, Sunset, Forest | Drifting colour only |

## Music reactivity

Tap **Music** in the settings panel — the toggle right next to Fullscreen and Timer — and the whole scene breathes with whatever is playing in the room. It is off until you switch it on, and tapping again switches it back off.

**Every mode reacts**, because the hook sits on the colour wash that all nine palettes share: the drifting blobs swell and brighten on the bass. The three animated modes add their own response on top — flames grow and throw extra embers in Fireplace, stars shimmer with loudness in Starfield, both in Campfire Sky.

It works by listening through the device microphone, so it reacts to any source: Spotify on a speaker, a phone, a record player. There is no Spotify sign-in, and there cannot be — the Spotify SDK's audio is DRM-protected and cannot be analysed, and Spotify's beat-data API has been closed to new apps since late 2024.

Nothing is recorded and nothing leaves the device: the microphone stream only reaches an `AnalyserNode` that is connected to no output.

Notes:

- Needs HTTPS. The GitHub Pages URL above qualifies; a local `file://` copy does not.
- On iPhone, a home-screen (standalone) launch needs **iOS 16.4 or newer** for the microphone to work. On older iOS, use it in Safari directly.
- iOS shows a recording indicator while it listens, and may ask for permission again each time you launch the app. That is the operating system, not this page.
- The microphone costs battery, which is why it is an explicit toggle and starts off.

## Deploying your own copy

1. Create a new public repository on GitHub.
2. Upload every file in this folder to the repository root (Add file → Upload files, drag the whole batch in).
3. Settings → Pages → Source: **Deploy from a branch**, branch **main**, folder **/ (root)**, Save.
4. After a minute or two the site is at `https://<your-account>.github.io/<repo-name>/`.

## Adding it to a phone home screen (this is what makes it fullscreen)

- **iPhone:** open the URL in Safari → Share → Add to Home Screen. Launched from that icon, there is no address bar.
- **Android:** open in Chrome → menu → Install app / Add to Home screen.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app — markup, styles and script in one file |
| `manifest.webmanifest` | Makes it installable, fullscreen and landscape by default |
| `sw.js` | Offline cache, so it opens with no network once installed |
| `icon-192.png` / `icon-512.png` | Home-screen icons |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is |

## After editing

When you change `index.html`, bump `ambient-v2` on the first line of `sw.js` to `ambient-v3` (a new number every time), or devices that already installed it keep serving the cached copy.
