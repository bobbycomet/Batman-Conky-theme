# ArkhamOS/Batcomputer Conky HUD

A Batman-themed Conky dashboard that fills the screen. Live system stats sit alongside a glowing bat-signal hologram, a real calendar, and a few Gotham-flavored decorative panels.

## What it shows

- **Bat-signal** (center) — color and flicker follow system health: blue when calm, amber on warning, red when something is critical
- **Threat Level** — Nominal/Elevated/Maximum (summary of the same health data)
- **Vitals** (left) — CPU, GPU, RAM, and disk as console-style readouts with bars
- **Calendar** (right) — the actual current month, with today highlighted
- **Weather with location** (screenshots have my location redacted; the red line is not part of the theme)
- **Moon phases** Because Batman needs to know how dark it will be
- **Villain Case File** — revolving profiles of Joker, Harley Quinn, Bane, Mr. Freeze, Penguin, Riddler, Poison Ivy, and Catwoman for immersion
- **Gotham Watch** & **Data Stream** — pure atmosphere (green text so you can tell them apart from real data)

<img width="1920" height="1080" alt="Screenshot_20260724_083124" src="https://github.com/user-attachments/assets/af9d19fb-b7ea-4dec-8432-352722ac4347" />
<img width="1920" height="1080" alt="Screenshot_20260724_144435" src="https://github.com/user-attachments/assets/10107d94-9b31-411b-ab86-f7c55a866b77" />

All the real telemetry (CPU, GPU, RAM, disk, weather, network, etc.) comes from the same backend as the Iron Man theme. Only the look is different.

## Requirements

- Conky with Lua + Cairo
- A compositor (for transparency)
- `curl`, `lm-sensors`
- GPU tools (`nvidia-smi` or AMD sysfs)
- Fonts: **Share Tech Mono** and **Orbitron**
- Optional: `smartctl` for disk temperature
- Tested on Kwin

## Install

```
Extract the tar.gz in ~/.config/conky

```

Or the manual way

```
mkdir -p ~/.config/conky
cp -r Batman ~/.config/conky/Batman
chmod +x ~/.config/conky/Batman/weather.sh \
         ~/.config/conky/Batman/sensors.sh \
         ~/.config/conky/Batman/start.sh
```

It uses its own cache and lock file.

## Launch

```bash
~/.config/conky/Batman/start.sh
```

Always start it this way (not with `conky -c` directly). Re-running the script cleanly replaces any previous instance.

Optional update intervals:

```bash
WEATHER_UPDATE_INTERVAL=900 SENSORS_UPDATE_INTERVAL=2 ~/.config/conky/Batman/start.sh
```

## Screen size

Default layout is for **1920×1080**.  
Edit `WIDTH` and `HEIGHT` near the top of `conky.conf` if your resolution is different.

## Quick customization

Open `batcomputer.lua` and look at the `CFG` table at the top:

| Setting | Purpose |
|---------|---------|
| `NET_IFACE` | Network interface (`'auto'` is fine) |
| `HAS_BATTERY` / `BATTERY_DEVICE` | Turn on for laptops |
| `THRESH` | Warning / critical thresholds |
| `COL_PRIMARY` / `COL_ACCENT` / `COL_WARN` | Colors for real data |
| `COL_INTERCEPT` | Color for the decorative panels |
| `MOON_SOUTHERN_HEMISPHERE` | Flip if the moon looks backwards |
