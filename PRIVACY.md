# 🛡️ Privacy Policy: ADAS Pro Nav (Mobile Edge AI + Navigation)

**Last updated:** 15 November 2026

This policy explains how **ADAS Pro Nav** (the web app) and its companion **ADAS Pro: Mobile Edge AI Vision System** handle data. They are research and teaching prototypes by the **Asari-Rashidi Energy Model Research Group**, built with a "Privacy by Design" approach: the AI runs on your own device, there is no account, no analytics, and no developer server that receives your data.

---

### 1. What stays on your device
* **Camera:** Used for lane detection and object detection (vehicles, pedestrians, animals, traffic lights/signs). Frames are analysed in memory by TensorFlow.js (COCO-SSD), in the page or in a background Web Worker on your device. Video is **never recorded, saved or uploaded**.
* **GPS location:** Used for speed, map speed limit, over-speed warning and turn-by-turn guidance. Location is **not stored** and is not sent to the developer.
* **Speech output:** Voice alerts and navigation prompts use your browser's built-in speech synthesis. The app does **not** record your voice or use the microphone.
* **Settings:** Your preferences (language, thresholds, Performance mode, mini-map, etc.) are saved in your browser's local storage on your device only. Clearing site data removes them.

### 2. Network requests the app makes
The app has no backend of its own, but your browser contacts these public services:

| Service | Purpose | What it receives |
|---|---|---|
| jsDelivr CDN (and the model host used by COCO-SSD) | Download TensorFlow.js, COCO-SSD and model weights | Standard web request data (your IP address, browser type) |
| Overpass API (OpenStreetMap; `overpass-api.de`, `overpass.kumi.systems`) | Look up the speed limit and road name near you | Your **approximate current coordinates** (throttled queries) |
| Nominatim (OpenStreetMap) | Search for a destination | The **text you search for** (and nearby bias, if used) |
| OSRM public demo server (`router.project-osrm.org`) | Calculate a driving route | **Your current position and the destination coordinates** |

These services are operated by third parties and have their own privacy policies and usage limits. Because they receive coordinates or search text, they may log them according to their own policies. If you do not want this, don't use route search / map speed limit (these can be switched off in Settings), and the AI vision features will still work.

### 3. What we do NOT do
* No video, image or location logs are sent to or stored by the developer.
* No advertising, tracking cookies, analytics or user profiling.
* No sale or sharing of data.

### 4. Hosting
The app is a static web page hosted on GitHub Pages (and, for the earlier edition, Streamlit Cloud). The hosting providers may keep ordinary server logs (such as IP address and request time) under their own policies. The vision engine runs entirely in your browser.

### 5. Your control
* Revoke **Camera** or **Location** at any time in your browser's site settings, or stop the app by closing the tab.
* Clear saved preferences by clearing site data for the page.
* Session-based: when the tab is closed, all temporary processing data is discarded.

### 6. Safety notice
This is an educational prototype, **not** a certified safety system. It must not replace attention to the road. Distances, speed limits and warnings are estimates and may be wrong. Please follow local traffic law and use a phone mount. Do not operate it while driving.

### 7. Children
The app is not directed at children and collects no personal information from anyone.

### 8. Changes
This policy may be updated as the app changes; the date at the top shows the latest revision.

### 9. Contact & metadata
* **Project:** ADAS Pro Nav / ADAS Pro: Mobile Edge AI Vision System
* **Organization:** Asari-Rashidi Energy Model Research Group
* **Lead Developer:** Mohd Rashidi Asari (GitHub: RashidiA)
* **License:** MIT License (see `LICENSE`)
* **Map data:** © OpenStreetMap contributors (ODbL)
