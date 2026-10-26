FORM / FRAME — VIDEO RECONSTRUCTION TOOL

FILES
- index.html: interface
- style.css: styling
- script.js: video sampling, shape rendering, colour controls, playback and export
- patterns/manifest.json: local pattern library index

RUN
Because browsers restrict fetch() from file:// pages, run this folder through a local server.
For example, in this folder run: python3 -m http.server 8000
Then open http://localhost:8000

PATTERN LIBRARY SETUP (important)
The supplied Google Drive URL identifies a folder, but this static browser app cannot reliably enumerate/download the folder's contents from the folder link alone. It does not use uploaded user patterns or invent substitute patterns. To use only your library:
1. Open the shared Drive folder and download/export the pattern image files into this patterns/ folder.
2. Edit patterns/manifest.json. Add each filename and its representative RGB colour:
   {"patterns":[{"src":"pattern-a.png","color":[220,80,90]},{"src":"pattern-b.png","color":[40,110,210]}]}
3. Keep all files from that approved library; the app will choose the closest pattern colour to each region.
For privacy/access, ensure you have permission to use the images. The Drive folder itself must be publicly viewable for other people to download the assets.

CURRENT IMPLEMENTATION NOTES
- Shape mode groups nearby sampled cells with similar colours and scales marks according to group size, up to 150 px. This is an approximation of the requested 1/4/9/16/25-cell mapping; the output is a stylised reconstruction, not a perfect segmentation algorithm.
- Pixelation slider controls sampling resolution.
- Colour shift and saturation alter sampled colours.
- Pattern mode maps sampled colour to nearest representative pattern colour.
- Face preservation uses a deliberately conservative skin-tone heuristic, not a reliable face-recognition model. If you need dependable face protection, add a dedicated client-side face detector.
- Export frame downloads the currently rendered frame as PNG. Video playback is live in the canvas, but exporting a full processed video requires a separate encoder pipeline (e.g. ffmpeg.wasm) and is not included in this initial build.
