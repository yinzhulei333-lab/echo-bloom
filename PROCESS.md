# PROCESS.md

## Starting idea

My first interactive piece was a pinball machine that decides things for you — input, physics, feedback. For this second piece I wanted a different kind of interaction, the kind you *feel* rather than operate: instead of clicking buttons, the piece should react to **your body and your voice in the room**. The starting image was a dark garden that only comes alive when someone is in front of it: shouting makes flowers burst, moving your hands stirs glowing wind, and holding the air then letting go releases everything at once.

The design question that shaped every later decision: *how do you make a screen feel like it is listening?* My answer was to keep the screen nearly empty when nobody interacts (just drifting dust), so that the first sound or movement produces an unmistakable cause-and-effect — the emptiness makes the response legible.

## Design / code changes made during development

1. **Voice mapped to two independent dimensions.** A first version only used loudness, so every shout looked the same. I added a spectral-centroid calculation: loudness drives the *size* and count of the bloom, while the tone drives the *hue* — low rumbles bloom blue-green, bright sounds bloom violet-pink. The same volume now looks different depending on what you actually said.
2. **Motion as paint instead of as a silhouette.** Showing a camera feed (or a stick figure) felt like a mirror, not an artwork. I switched to frame-differencing on a tiny 80×60 offscreen canvas and used only the *changed* pixels: your movement becomes glowing trails, mirrored so it feels like your own space. Nothing is recorded; frames are discarded immediately.
3. **"Grab and release" without hand tracking.** Full hand tracking would need a model and a powerful machine. Instead I approximated the gesture by watching motion energy: sustained movement arms the gesture, and a sudden stop "releases" one large bloom at the centroid of where you were moving. It reads as grabbing the air and letting it go.
4. **Graceful degradation as a feature, not a fallback.** Camera and microphone are opt-in toggles, and permission denial produces a calm message plus a fully working mouse mode (move to stir, click to bloom). This was important because the piece must never look broken in a gallery or on a marker's machine without a webcam.
5. **Idle breathing.** After nine seconds of stillness the garden blooms on its own, so an unattended screen still invites a passer-by to interact.

## User trial

*(Do this before submitting: ask someone to try it, then fill in the three lines below.)*

- **Who tried it:** e.g. a flatmate (not identified).
- **What I observed:** e.g. they clicked the mouse first, then asked what the buttons were for; they shouted once, laughed at the bloom, then tried a long note to see if the colour changed; they did not discover the grab-and-release gesture on their own until I hinted at it.
- **One improvement I made because of the trial:** e.g. after seeing the gesture go undiscovered, I added the instruction line to the on-screen status text, and made the first bloom after loading larger so the cause-and-effect is obvious within one second. *(Replace with what actually happened and what you actually changed, or explain why you kept the design.)*

## AI tools used

- **What I used AI for:** drafting the particle system and the audio/camera plumbing, discussing how to map sound to colour, and editing this document.
- **One suggestion I kept:** the idle "breathing" blooms that appear when nobody touches the piece — the AI pointed out a generative artwork needs to look alive before interaction, which I had not considered.
- **One suggestion I rejected:** the AI first proposed drawing a live camera silhouette behind the particles. I rejected it: it turns the piece into a mirror and makes the interaction about *you* rather than about the garden.

## Credits

- All code written for this project (with AI assistance as described above). No libraries, no external assets, no datasets. Techniques used — additive blending, frame-differencing motion detection, Web Audio RMS and spectral centroid — are standard, implemented here from scratch.
- Privacy: camera and microphone streams are processed entirely in the browser; nothing is uploaded or stored.
