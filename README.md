# Cam Gradient

Live mesh gradients made from the colors your webcam (e.g. the Mac FaceTime camera) sees.
Inspired by photogradient.com, but it uses a live camera feed instead of an uploaded photo.
It's one self-contained `index.html` with no dependencies, no CDNs, and no network calls. Nothing leaves your machine.

## Run

**Chrome:** double-click `index.html` (it works from `file://`), click **Start camera**, and allow access.

**Safari (or any browser that blocks the camera on file://):** serve the folder on localhost:

```bash
cd cam-gradient
python3 -m http.server 8000
# open http://localhost:8000
```

If the camera is blocked, open macOS System Settings → Privacy & Security → Camera and turn it on for your browser.

## Features
- **Start camera** button with clear messages for denied, missing, busy, or unsupported cameras. If you have more than one camera (FaceTime, Continuity Camera, USB), a picker appears.
- Frames are downscaled to 48×36 about 9 times a second. k-means in OKLab picks 2–6 dominant colors. Each run starts from the previous centroids, so every color keeps its slot, and colors ease toward new values over time, so the gradient flows instead of flickering.
- WebGL shader: a mesh (inverse-distance blend of drifting color points, mixed in OKLab), plus Linear and Radial styles. Domain warp and film grain are included. A Canvas2D fallback runs automatically (force it with `?renderer=2d`).
- Controls (click the header to collapse): style, number of colors, smoothness, vibrance, freeze colors, speed, softness, warp, grain, and a camera preview thumbnail.
- Palette swatches show hex codes. Click one to copy it.
- Export: **Save PNG** at screen size, HD, QHD, 4K, MacBook, iPhone, or square. **Copy CSS** copies a CSS gradient for the current style: layered radial-gradients for mesh, or a linear/radial gradient.

## Keys
`Space` freeze colors · `H` hide UI · `F` fullscreen · `S` save PNG · `Esc` close message

## Console
`camGradient.palette()`, `camGradient.css()`, `camGradient.exportPNG()`
