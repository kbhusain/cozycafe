[README.md](https://github.com/user-attachments/files/34727047/README.md)
# ☕ Cozy Soundscape — Ambient Noise Mixer & Music Companion

A lightweight, responsive, single-page ambient sound mixer built with semantic HTML5, Tailwind CSS, the browser's native **Web Audio API**, and standard HTML5 audio streaming. 

Designed for deep focus, studying, relaxation, and reading, it lets users mix and match coffeehouse and park ambient sounds with customizable volumes, strike rates, real MP3 audio loops, and background music.

---

## 📁 Project Structure

```text
cozy-soundscape/
├── index.html        # Complete application source code (HTML, CSS, JS, Audio Engine)
├── audio/            # Full-length offline audio assets
│   ├── gentle-rain-ambient.mp3                     # 10-minute high-quality rain recording
│   └── conversation-background-noise-358083.mp3    # 13-minute authentic cafe chatter recording
└── README.md         # Documentation, architecture guide, customization, and deployment manual
```

---

## ⚡ Features

1. **7 Ambient Audio Channels**:
   - 🌧️ **Gentle Rain**: Dual mode (real 10-minute recorded audio loop or procedural pink noise).
   - ⛈️ **Rolling Thunder**: Synthesized resonant sub-bass rumble with variable strike frequency (1 to 60 per minute) and an on-demand "⚡ Strike Thunder" button.
   - ☕ **Warm Cafe Hum**: Low room tone and air texture modeling a quiet cafe interior.
   - 💨 **Barista Steam & Espresso**: Periodic frothing hisses and espresso steam bursts.
   - 🍽️ **Dishes in Sink**: Multi-impact acoustic porcelain clatter modeling plate bodies, glaze rings, and stainless steel sink damping.
   - 👥 **Soft Chatter**: Dual mode (real 13-minute cafe conversation recording or formant-filtered room murmur).
   - 🚗 **Distant Traffic**: Low-frequency rolling vehicle rumble modulated with a slow LFO.

2. **Universal MP3 File Pickers (`📁 Choose MP3`)**:
   - Every sound channel includes a custom file picker.
   - Select any local MP3 file to stream and loop it in-memory via `URL.createObjectURL()` without uploading to a server.

3. **Master Control Bar**:
   - Master Play / Pause with instant hardware suspension.
   - Master volume slider (0% to 100%) that scales all channel levels synchronously.
   - Mobile & iOS Safari optimized with hardware audio context suspension and touch-action listeners.

4. **Curated Presets**:
   - **🌧️ Rainy Cafe**: Rain, Thunder, Cafe Hum, Steam, and Dishes activated.
   - **🌳 Sunny Park**: Soft Chatter and Distant Traffic activated.
   - **Reset**: Instantly silences all channels.

5. **Spotify Music Companion**:
   - Embedded web player for streaming lo-fi, acoustic, jazz, and peaceful piano playlists directly alongside your ambient noise mix.
   - Custom URL parser accepting any playlist, album, or track link from `open.spotify.com`.

6. **Google AdSense Ready**:
   - Pre-configured responsive leaderboard placeholders (mid-page and footer).
   - Staged publisher script in `<head>` ready to activate when approved.

---

## 🛠️ How to Customize & Modify Audio Files

### 1. Setting Permanent Default MP3s for Existing Channels
1. Drop your `.mp3` file into the `audio/` folder (e.g. `audio/thunder-storm.mp3`).
2. Open `index.html` and search for `const channelAudios`:
   ```javascript
   const channelAudios = {
     rain: new Audio('./audio/gentle-rain-ambient.mp3'),
     thunder: new Audio('./audio/thunder-storm.mp3'), // Add your path here
     ...
   };
   ```
3. Set the channel's default mode to `'mp3'` in `const channels`:
   ```javascript
   thunder: { enabled: false, volume: 0.6, frequency: 12, mode: 'mp3', nodes: {} }
   ```

### 2. Adding a New Sound Channel (e.g. "Campfire" 🪵)
1. In `index.html`, copy any existing sound card `<div>` in the grid and replace the ID prefixes with your new name (e.g., `fireToggle`, `fireVolume`, `fireSubtitle`, `fireFileInput`).
2. In `<script>`, register the new audio element and channel state:
   ```javascript
   channelAudios.fire = new Audio('./audio/crackling-fire.mp3');
   channelAudios.fire.loop = true;
   channels.fire = { enabled: false, volume: 0.5, mode: 'mp3', nodes: {} };
   channelColors.fire = 'amber';
   ```
3. Register the UI listeners:
   ```javascript
   // In channelControls:
   fire: setupChannel('fire', 'Fire', 'Playing Fire Audio'),

   // In channelIds array:
   const channelIds = ['rain', 'thunder', 'cafe', 'steam', 'clink', 'chatter', 'traffic', 'fire'];
   ```

---

## 🚀 How to Deploy Your App (Free)

### Method 1: Netlify Drop (Easiest — 10 Seconds, No Account Needed)
1. Unzip `cozy-soundscape-source-code.zip`.
2. Go to [https://app.netlify.com/drop](https://app.netlify.com/drop) in your browser.
3. Drag and drop the unzipped `cozy-soundscape` folder onto the web page.
4. Netlify will publish your site instantly and give you a public `https://<site-name>.netlify.app` link.

### Method 2: GitHub Pages (Permanent & Version-Controlled)
1. Go to [GitHub](https://github.com/) and create a new public repository named `cozy-soundscape`.
2. Upload `index.html`, the `audio/` folder, and `README.md`.
3. Go to **Settings** > **Pages**.
4. Set the source branch to `main` (or `master`) and folder to `/ (root)`, then click **Save**.
5. Your site will be live at `https://<your-username>.github.io/cozy-soundscape/`.

### Method 3: Cloudflare Pages or Vercel
1. Log in to [Cloudflare Pages](https://pages.cloudflare.com/) or [Vercel](https://vercel.com/).
2. Connect your GitHub repository or drag-and-drop the project folder.
3. Keep default settings (Framework preset: *None / Other*) and click **Deploy**.

---

## 📱 Mobile & Browser Compatibility

- **Web Audio API**: Procedural noise buffers and filters are generated on the client side using standard AudioContext nodes.
- **iOS Safari Touch & Pause Fix**: Hardware audio session is explicitly halted via `audioCtx.suspend()`, gain zeroing, and touch-event protection to guarantee reliable pause behavior on iPhones and iPads.
- **Offline Capable**: Double-clicking `index.html` on any computer runs the application locally in Chrome, Safari, Firefox, or Edge without requiring an internet connection.
