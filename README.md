# WaxOff — Stereo Podcast Leveler

WaxOff sets **final program loudness** and exports deliverables after editing. It uses a two‑pass EBU R128‐style loudness normalization (ffmpeg `loudnorm`) with a **true‑peak ceiling of −1 dBTP** and common targets like **−18 LUFS** or **−16 LUFS**.

> Use **WaxOn** *before editing* to produce clean, unclipped mono WAVs for the DAW. Use **WaxOff** *after editing* to hit delivery targets.

---

## Install (one‑liner)

Installs to `~/WaxOff` and symlinks `waxoff` into `~/bin` (or `~/.local/bin`):

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/sevmorris/WaxOff/main/install.sh)"
```

If a proxy/CDN is serving a cached copy, try this cache‑busting variant:

```sh
/bin/bash -c "$(curl -fsSL "https://raw.githubusercontent.com/sevmorris/WaxOff/main/install.sh?nocache=$(date +%s)")"
```

Ensure your shell can find `~/bin` (or `~/.local/bin`):
```sh
# zsh
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc && exec zsh
# bash
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bash_profile && source ~/.bash_profile
```

---

## Usage (quick start)

```sh
waxoff *.wav
```
Typical prompts (or flags/envs if non‑interactive):
- Loudness target (e.g., −18 or −16 LUFS)
- True‑peak ceiling: −1 dBTP
- Output: WAV, MP3 (128/160/192), or Both
- Sample rate: 44.1 kHz (default) or 48 kHz

---

## Troubleshooting

- **`BASH_SOURCE[0]: unbound variable`** — You pulled a cached installer. Re‑run the cache‑busting one‑liner above.
- **`waxoff` not found** — Add `~/bin` (or `~/.local/bin`) to your PATH (see Install section).
- **`ffmpeg: command not found`** — Install ffmpeg first (macOS: `brew install ffmpeg`).

---

## License

MIT © Seven Morris
