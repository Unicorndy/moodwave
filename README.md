```text
███╗   ███╗ ██████╗  ██████╗ ██████╗ ██╗    ██╗ █████╗ ██╗   ██╗███████╗
████╗ ████║██╔═══██╗██╔═══██╗██╔══██╗██║    ██║██╔══██╗██║   ██║██╔════╝
██╔████╔██║██║   ██║██║   ██║██║  ██║██║ █╗ ██║███████║██║   ██║█████╗
██║╚██╔╝██║██║   ██║██║   ██║██║  ██║██║███╗██║██╔══██║╚██╗ ██╔╝██╔══╝
██║ ╚═╝ ██║╚██████╔╝╚██████╔╝██████╔╝╚███╔███╔╝██║  ██║ ╚████╔╝ ███████╗
╚═╝     ╚═╝ ╚═════╝  ╚═════╝ ╚═════╝  ╚══╝╚══╝ ╚═╝  ╚═╝  ╚═══╝  ╚══════╝
```

# Moodwave

An interactive, audio-reactive visualizer built in a single HTML file.

`index.html` renders a grid of 101 algorithm/mood cards that react to audio in real time. You can drive it with built-in procedural loops, uploaded audio files, microphone input, or browser tab audio.

## What this page does

- Shows a responsive grid of visual cards, each with a unique algorithm and mood styling.
- Reacts visuals to bass, mid, treble, and beat energy from live audio analysis.
- Supports focus and fullscreen zoom for a single visualizer.
- Includes a mini player with:
  - Play/pause
  - Previous/next
  - Track select
  - Loop modes (`all`, `one`, `off`)
  - Scrubber seek
  - Playlist chips for uploaded tracks
- Supports background customization:
  - Animated gradient themes
  - Optional wallpaper image with fit modes (`fill`, `stretch`, `retain`)

## Quick start

### Option A) Download and open directly

- Download `index.html`.
- Double-click it (or drag it into any browser) to run immediately.

This works for core visuals and built-in loops in any modern browser. For microphone and tab-audio capture, use `localhost` or `https` (secure context) for reliable permissions.

### 1) Open the project

From this folder, run a local web server (recommended for media permissions):

```bash
python3 -m http.server 8000
```

Then open:

- `http://localhost:8000/index.html`

You can also open the file directly, but microphone/tab capture is usually blocked or unreliable unless the page is served from a secure context (`https` or `localhost`).

### 2) Start audio

Use one of these options:

- Click `Play` to start built-in generated loops.
- Click `Add music` to import local audio files.
- Click `Mic` to visualize microphone input.
- Click `Tab audio` to capture browser/tab sound.

### 3) Interact with visuals

- Click a card once: focus mode (other cards dim).
- Click the same focused card again: fullscreen zoom view.
- Press `Esc`: exit zoom (or clear focus if not zoomed).

## Deploy on GitHub Pages

Use these steps to host the visualizer publicly:

1. Push this project to a GitHub repository.
2. In your repository, open `Settings` -> `Pages`.
3. Under `Build and deployment`, set:
  - `Source`: `Deploy from a branch`
  - `Branch`: `main` (or your default branch)
  - `Folder`: `/ (root)`
4. Click `Save`.
5. Wait for Pages to build, then open the URL GitHub shows (usually `https://<username>.github.io/<repo>/`).

If your entry file is `index.html` in repository root, GitHub Pages serves it automatically as the site homepage.

### GitHub Pages notes

- `Mic` and `Tab audio` typically work better on GitHub Pages than local file-open mode because Pages is served over `https`.
- If updates do not appear, hard refresh the page (`Cmd+Shift+R` on macOS).

## How to use (controls)

- `Play`: toggles play/pause for the selected track.
- `Prev` / `Next`: navigates across available track options.
- Track dropdown: selects current source track.
- `Loop` button cycles:
  - `all` (loop entire playlist)
  - `one` (repeat current track)
  - `off` (stop at end of playlist)
- `Add music`: imports multiple files and appends them to playlist.
- Playlist chips:
  - Click chip: play that track.
  - Click `x`: remove track from playlist.
- `Mic`: toggle live microphone visualization.
- `Tab audio`: toggle live tab audio visualization.
  - In the picker, choose a tab and enable share-tab-audio.
- `BG`: opens background panel.
  - Pick animated theme swatches.
  - Upload a wallpaper image.
  - Change wallpaper fit mode.
  - Clear wallpaper.
- Scrubber bar: click to seek within current track.

## Extra developer notes

- All logic is self-contained in `index.html` (HTML, CSS, JS).
- Motion library is loaded from CDN (`motion` ESM via jsDelivr).
  - If CDN load fails, page still runs with reduced animation flourishes.
- Visualizers are viewport-culled with `IntersectionObserver` for better performance.
- Idle mode generates synthetic audio data so visuals stay alive before playback.
- `#test` hash runs built-in assertions:

Open:

- `http://localhost:8000/index.html#test`

Then check browser console for self-test results.

## Browser permissions and troubleshooting

- No mic/tab input:
  - Confirm browser permission prompts were allowed.
  - Use `localhost` (not random insecure origins).
- Tab audio has no sound:
  - Re-open capture and enable share-tab-audio in picker.
- Uploaded file fails:
  - The app shows decode failures in the error message area.
- Stutter on slower machines:
  - Reduce simultaneous activity (avoid zoom + heavy tab audio + many background effects).

## Files

- `index.html`: complete app implementation.
- `sound_visualization_algorithms_handover.md`: algorithm handover documentation.
- `docs/`: additional plans/specs.
