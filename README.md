# MotorScan — 3-Phase Induction Motor Analyzer

Web app that uses your phone camera + OCR to read motor nameplates and compute electrical/mechanical values.

## Features
- Live camera capture (rear cam preferred) or image upload
- OCR via [Tesseract.js](https://tesseract.projectnaptha.com/) — no backend needed
- Auto-parses: Power (kW), Voltage (V), Current (A), Speed (rpm), cosφ, η
- Editable fields — correct anything OCR gets wrong
- Computes:
  - Electrical power input: `P_elec = √3 × U × I × cosφ`
  - Shaft torque: `T = P₂ × 9550 / n`
  - Efficiency check vs nameplate η

## Quick Start (local development)

```bash
# Clone or create your project folder
mkdir motorscan && cd motorscan

# Copy index.html here, then serve locally (pick one):
npx serve .
# or
python3 -m http.server 8080
# or
npx http-server -p 8080

# Open http://localhost:8080
```

> **Note:** Camera access requires HTTPS in production. For local dev, `localhost` is treated as secure by browsers.

## Deploy to GitHub Pages

```bash
cd motorscan
git init
git add index.html README.md
git commit -m "feat: initial MotorScan release"

# Create repo on GitHub (github.com/new), then:
git remote add origin https://github.com/YOUR_USERNAME/motorscan.git
git branch -M main
git push -u origin main
```

Then in your repo → **Settings → Pages → Source: main / (root)**.

Your app will be live at:  
`https://YOUR_USERNAME.github.io/motorscan/`

## Usage Tips

1. **Good lighting** on the nameplate improves OCR accuracy significantly
2. Hold phone **parallel** to the label (avoid angle distortion)
3. If OCR misreads a value, simply **edit the field** and click CALCULATE
4. The app works entirely **client-side** — no data leaves your device

## Tech Stack

| Library | Version | Purpose |
|---|---|---|
| Tesseract.js | 4.1.1 | In-browser OCR |
| Google Fonts | — | Typography (Share Tech Mono + Barlow Condensed) |

No build tools, no dependencies to install. Pure HTML + vanilla JS.

## Formula Reference

| Quantity | Formula | Units |
|---|---|---|
| Electrical Power | `P = √3 × U × I × cosφ` | kW |
| Torque | `T = P₂ × 9550 / n` | Nm |
| Efficiency | `η = P₂ / P_elec × 100` | % |
