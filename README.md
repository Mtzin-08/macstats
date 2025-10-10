# MacStats MVP (Python, macOS menu bar)

A tiny, configurable **menu bar** app for macOS written in Python. Choose which stats to show with simple checkboxes in the app menu. No windows. No fluff.

**Modules available**
- CPU usage
- Memory usage
- Network rate (upload / download)
- Disk free space
- Battery percent (+ charging indicator)
- GPU (experimental; requires parsing `powermetrics`, typically needs `sudo` on Apple Silicon)

## Quick start

```bash
# Create a venv (recommended)
python3 -m venv .venv
source .venv/bin/activate

# Install deps
pip install -r requirements.txt

# Run
python3 main.py
```

Grant **Accessibility** permission for the terminal you run from if macOS prompts you (rumps embeds a status item; usually no special permission is needed for reading stats, but prompts can vary).

Config is stored at `~/.macstats_mvp/config.json` after you hit **Save settings** in the app menu.

## Packaging into a .app (optional)
You can use `py2app` if you want a double‑clickable `.app`:

```bash
pip install py2app
python3 setup.py py2app
open dist/MacStats\ MVP.app
```

> Note: First launch of unsigned apps may require right‑click → Open.

## How it works

- **rumps** creates a single menu bar item whose title is a compact string of your selected modules.
- **psutil** reads CPU, memory, disk, battery, and network counters.
- Network **rate** is computed by sampling byte counters and converting to bytes per second.
- **GPU** is a placeholder; enabling it tries to parse `powermetrics --samplers gpu_power -n 1` output. For accurate data, you’ll likely need to run a privileged helper and cache samples at a lower frequency.

## Roadmap ideas
- Per‑core CPU and memory pressure indicator
- Per‑process top talkers for network (sampling `nettop`)
- A compact icon set with symbols instead of text
- Optional multi‑item mode (separate status items per module via PyObjC)
- Export snapshot to clipboard
- Configurable update interval

## License
MIT
