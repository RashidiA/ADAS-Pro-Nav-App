# 🚗 ADAS Pro + Navigation

A phone-camera **driver-assistance demo** that runs entirely in the browser. It combines camera-based ADAS warnings with GPS speed and the **map speed limit** of the road you are on.

🌐 **Live app:** [https://rashidia.github.io/ADAS-Pro-Nav-App/](https://rashidia.github.io/ADAS-Pro-Nav-App/)

> ⚠️ **Driver-assistance demo for learning. Not certified, not a safety system, and not a replacement for driver attention.** Mount the phone safely and stay responsible for driving. Do not operate the app while driving.

---

## ✨ What it does

| Feature | How it works |
|---|---|
| **Vehicle, pedestrian, animal detection** | A small AI model (TensorFlow.js, coco-ssd) runs on the phone. Boxes show the object and an estimated distance. |
| **Collision warning** | Distance and time-to-collision are estimated from the camera. A banner, beep and vibration warn when a vehicle, person or animal is too close in your path. |
| **Blue lane overlay + lane-change warning** | The white lane markings are found on the video and drawn as a continuous blue lane. You are warned when the car drifts toward a line. |
| **Road signs and traffic lights** | Stop signs and traffic lights are detected (red, yellow or green is read from the light). Speed-limit signs are supported through an optional custom model. |
| **GPS speed** | Shown on screen. Lane warnings are muted at low speed. |
| **🆕 Map speed limit** | Your position is matched to the nearest road in [OpenStreetMap](https://www.openstreetmap.org/) and its `maxspeed` is shown on a speed-limit sign badge with the road name. |
| **🆕 Over-speed warning** | A warning appears after 2 seconds above the limit plus a margin (default 5 km/h). A fresh camera-read sign overrides the map for 20 seconds. If the sign and the map disagree by 20 km/h or more, the app says "check". |
| **Settings (⚙)** | Sound, vibration, map limit on or off, over-speed margin, horizon, bonnet cut-off and camera field of view. Saved in the browser. |

Alerts have priorities, so a collision warning always takes the banner before a lane or over-speed message.

---

## 📱 How to use

1. Open the live link on your phone (Chrome on Android or Safari on iPhone) over **HTTPS**.
2. Tap **START ADAS** and allow **camera** and **location**.
3. Mount the phone at the centre of the windscreen with the camera level with the road.
4. Use **Set centre** to calibrate the lane position and **Lane change** to mute lane warnings when you change lanes on purpose.
5. Open **⚙** to adjust settings.

Tips:
* The AI model and TensorFlow.js load from the internet the first time, so the first start takes a few seconds.
* Good light and a clean windscreen improve detection.
* Use the landscape orientation for a wider view.

---

## 🗺️ About the map speed limit

* Data comes from OpenStreetMap through the free **Overpass API**. The app asks at most once every 8 seconds, to stay within fair use.
* The nearest road is chosen using your position and heading. Footpaths and cycle paths are ignored.
* **Many roads have no speed limit tagged.** When that happens the badge shows `--` and the text says no limit is tagged in the map. This is a gap in the map data, not an app fault.
* GPS can be off by 10 m or more in cities, so at junctions the app may briefly show the wrong road.
* A mobile data connection is needed for the map lookup.

---

## 🧠 How it works (short version)

* **Detection:** coco-ssd (lite MobileNet v2) runs about 15 times per second on a small 320 px image.
* **Lane:** scan lines on a 320 px image find white paint, fit the left and right lane lines, and smooth them over time.
* **Distance:** estimated from the object's real height, the camera field of view and the box height.
* **Map limit:** Overpass returns nearby roads with their tags. The closest segment with a matching direction wins.
* Everything runs on the phone. Only the map lookup sends your approximate position to the Overpass server.

---

## 📂 Files

```text
├── index.html   # The whole app: page, styles, detection, lane, GPS and map-limit code
└── README.md    # This file
```

No build step. To run locally, serve the folder over HTTPS or on `localhost` (camera and GPS need a secure context), for example `python3 -m http.server` and open `http://localhost:8000`.

---

## 🚀 Publish with GitHub Pages

1. Put `index.html` in the repository root.
2. Go to **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`, then save.
3. The app appears at `https://<your-username>.github.io/<repository-name>/`.

---

## 🛣️ Roadmap

1. ✅ Camera ADAS + GPS speed + map speed limit (this version)
2. ⬜ Route search, voice instructions and a next-turn arrow as a HUD
3. ⬜ Mirrored HUD mode, mini-map and lane guidance
4. ⬜ Custom speed-limit sign model for Malaysian road signs

---

## 🔗 Related projects

* [Smartphone ADAS Pro (Streamlit version)](https://smartphone-adaspro-app-2uumyn58jvniwsku8uspgu.streamlit.app/) · [source](https://github.com/RashidiA/Smartphone-ADASPro-App)
* [Automotive Simulation (student version)](https://rashidia.github.io/Automotive-simulation-student-version/) includes the ADAS Simulator for levels 0 to 5.
* [Automotive Knowledge Hub](https://rashidia.github.io/Automotive-Knowledge-Hub/)

---

## ⚠️ Disclaimer

This is a simplified teaching demo. Detection can miss or misjudge objects, distances are estimates, and map speed limits can be missing or out of date. Results are **not** for real driving decisions, safety certification or any commercial use. Always obey the posted speed limit and traffic rules.

---

## 🧩 Credits

* [TensorFlow.js](https://www.tensorflow.org/js) and the coco-ssd model.
* Map data © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright), available under the ODbL, served through the [Overpass API](https://overpass-api.de/).

## 👤 Author

Created by [RashidiA](https://github.com/RashidiA).
