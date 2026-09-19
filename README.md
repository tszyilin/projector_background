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

## Moving to the beat

Two ways to make the scene pulse in time with music. They are mutually exclusive — turning one on switches the other off.

### Beat slider (works with music on the same phone)

Drag **Beat** in the settings panel to roughly the tempo of what you are playing, and the whole scene pulses at that rate. All the way left is off.

This is the one to use on an iPhone that is also playing the music, because it uses no microphone at all — no permission prompt, no audio session, nothing that can interrupt Spotify.

It is a free-running metronome, not beat detection: it holds the tempo you set, so over several minutes it drifts out of phase with the song and it does not follow tempo changes. The pulse is a slow breath rather than a strobe, so this reads as ambience rather than as a clock that is wrong.

### Microphone (real sync, needs the music to come from elsewhere)

Tap **Music** and the scene follows whatever is actually audible in the room — genuinely in sync, reacting to the bass. Nothing is recorded and nothing leaves the device: the stream only reaches an `AnalyserNode` connected to no output.

**On iOS this will pause music playing on the same device.** `getUserMedia` switches the system audio session into record mode, which interrupts other apps. So use it when the music comes from a separate speaker, phone or laptop; if it is playing on the phone running this page, use the Beat slider instead. Android generally keeps playing. The app warns you once before it ever asks for the microphone.

Other notes:

- Needs HTTPS. The GitHub Pages URL above qualifies; a local `file://` copy does not.
- On iPhone, a home-screen (standalone) launch needs **iOS 16.4 or newer** for the microphone to work. On older iOS, use it in Safari directly.
- iOS shows a recording indicator while it listens, and may ask for permission again each time you launch the app. That is the operating system, not this page.
- The microphone costs battery, which is why it is an explicit toggle and starts off.

### What reacts

**Every mode**, because the hook sits on the colour wash that all nine palettes share: the drifting blobs swell and brighten on each beat. The three animated modes add their own response on top — flames grow and throw extra embers in Fireplace, stars shimmer with loudness in Starfield, both in Campfire Sky.

### Why there is no Spotify sign-in

There cannot be one. Spotify's Web Playback SDK serves DRM-protected audio that a web page is not allowed to analyse, and the API that used to hand out per-beat timestamps has been closed to new apps since late 2024. Listening to the room, or setting the tempo by hand, are the two routes that actually work.

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
