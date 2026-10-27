# ECHO BLOOM 🌬🌸

An interactive generative-art garden that responds to your **voice**, your **motion**, and your **hands** — built with vanilla HTML/CSS/JS and the Canvas API. No libraries, no accounts, no data leaves the device.

## The idea

This is not a game with a goal — it is an *instrument you play with your body*. A dark, quiet field of drifting dust that turns into a blooming garden the moment you interact with it:

- **🎙 Voice** — the microphone analyses volume and spectral centroid in real time. Shout, whisper, or sing: every loud moment bursts into a bloom whose *size follows your volume* and whose *colour follows your tone* (low rumbles bloom blue-green, bright sounds bloom violet-pink).
- **📷 Motion** — the camera runs lightweight frame-differencing (no ML, no face data stored): moving paints glowing trails in a mirrored "wind". **Grab & release gesture:** keep moving, then suddenly hold still and pull away — the garden releases everything you "held" in one big bloom.
- **🖱 Hands (always available)** — moving the mouse stirs trails; clicking blooms flowers. If camera/mic permission is denied or unavailable, the piece degrades gracefully to this mode and never becomes broken.

## Interaction loop

1. **Input** — sound (mic), motion (camera), or pointer.
2. **Response** — blooms, trails and halos are generated with particle physics (additive glow, drift, gravity, fade).
3. **Feedback** — every input has an immediate visible/audiovisual echo; the live volume meter and status line make the current inputs legible.
4. **Next action** — the garden keeps breathing (idle auto-blooms after 9s of stillness invite you back in).

## Permissions & privacy (deliberate error handling)

- Camera and microphone are **opt-in toggles**, never requested on load.
- Permission denied / device missing → a calm message explains the fallback; mouse interaction always works (the assignment's "denied permission" case is handled by design).
- Everything is computed locally — frames are diffed on a tiny 80×60 offscreen canvas and discarded; nothing is uploaded or stored. Stated in the footer.
- Toggling a sensor off immediately stops its stream (`getTracks().stop()`).

## How to run

No dependencies. Double-click `index.html`, or (recommended — camera/mic need a secure context):

```bash
cd echo-bloom
python3 -m http.server 8000
# open http://localhost:8000
```

Note: browsers expose getUserMedia only on `https://` or `localhost`. Opened as a plain `file://`, the mouse mode still works but the toggles will report that the sensors are unavailable.

## Known limitations

- Motion detection is frame-differencing, not skeleton tracking: it senses *where* you move, not hand shapes. The "grab & release" gesture is approximated as "sustained motion, then a sudden stop".
- Very dark rooms reduce camera sensitivity.
- Designed for desktop; on small screens it still works but the layout of controls is minimal.

## Credits

- All code, particle systems and visuals written from scratch for this project (with AI assistance for drafting). Generative-art conventions (additive blending, frame-diff motion detection, spectral centroid mapping) are common techniques, implemented originally here. No external assets, libraries or datasets.
