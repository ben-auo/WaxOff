# WaxOff — Final Mix Loudness Leveler (No Dynamics Processing)

**Purpose:** WaxOff sets the **final stereo mix** to a consistent broadcast/podcast loudness target **without changing tone or dynamics**. It performs *transparent, two‑pass BS.1770 / EBU R128 loudness normalization* using `ffmpeg`’s `loudnorm` and applies a **true‑peak safety ceiling of −1 dBTP**—*no EQ, no compression, no expanders, no gates*. Just level and go.

- **Targets:** −18 LUFS (default) or −16 LUFS
- **Safety:** true‑peak ceiling at −1 dBTP (no multiband or time‑varying compression)
- **Outputs:** 24‑bit WAV, CBR MP3 (128/160/192 kbps), **FLAC** (optional), or combinations
- **Sample rate:** choose **44.1 kHz** or **48 kHz**
- **Writes atomically:** hidden temp files until successful finalize
- **Interactive by default;** fully scriptable via flags/env

> For pre‑mix prep (mono channel‑0 WAV/FLAC, DC‑block, optional declip, and limiting for editing), see **WaxOn**.

---

## Install

Installs by cloning to your home directory and creating a symlink in `~/bin` (or `~/.local/bin`).

### Quick install
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/sevmorris/WaxOff/main/install.sh)"
```

This will:
1) Clone/update `~/WaxOff`
2) Symlink `waxoff` into `~/bin` (or `~/.local/bin`)

Ensure your shell can find the symlink:
```bash
# zsh
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc
# bash (macOS)
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bash_profile
```

### Uninstall (symlink only)
```bash
~/WaxOff/uninstall.sh
```
This removes the `waxoff` symlink but leaves the repo in `~/WaxOff`.

---

## Usage

### Interactive (recommended)
```bash
waxoff *.wav
```
You’ll be prompted for:
- Target loudness: **−18** or **−16 LUFS**
- Output mode: `wav` | `mp3` | `both` | `flac` | `wav+flac` | `all`
- MP3 bitrate (if chosen): **128k**, **160k** (default), **192k**
- FLAC compression level: 0–12 (default **8**)
- Sample rate: **44100** or **48000** Hz

### Non‑interactive
```bash
# flags
waxoff --no-prompt -t -18 -m wav+flac -s 48000 *.aif

# or via env
PROMPT=0 TARGET_I=-18 OUTMODE=all SAMPLE_RATE=48000 waxoff *.wav
```

#### Flags
```
-t, --target <LUFS>      -18 (default) or -16
-m, --mode <mode>        wav | mp3 | both | flac | wav+flac | all   (default: both)
-b, --bitrate <rate>     128k | 160k (default) | 192k  (MP3)
-s, --samplerate <hz>    44100 or 48000
    --flac-level <N>     0..12 compression (default: 8)
-l, --log <path>         Log file path (default: ~/Library/Logs/waxoff_cli.log)
    --no-prompt          Skip interactive questions
-q, --quiet              Reduce console output
-n, --dry-run            Show actions without writing files
```

---

## What it **does** / **doesn’t** do

- **Does:** two‑pass loudness normalization to **−18/−16 LUFS**, applies a **−1 dBTP true‑peak ceiling**, optional resample to 44.1/48 kHz, writes chosen deliverables (WAV/MP3/FLAC).
- **Doesn’t:** alter program dynamics or timbre. There’s **no** EQ, compression, multiband processing, gating, expansion, or “sweetening.” The only gain change is the **global** adjustment computed by EBU R128 analysis with a true‑peak safety margin.

---

## Dependencies

- `ffmpeg` (macOS: `brew install ffmpeg`)
- `bash`, `git`

---

## Typical workflow

1. **Edit/Mix in DAW** → bounce stereo mix at native rate.
2. **WaxOff** → set final program loudness (−18/−16 LUFS) and output WAV/MP3/FLAC as needed.
3. **Deliver** → upload to host/distribution.

---

## Troubleshooting

- **Output too loud/quiet?** Confirm your DAW export isn’t already clipped and that you selected the intended target (−18 vs −16).
- **Weird artifacts?** WaxOff is transparent; artifacts usually come from the source. Try re‑exporting your mix at 24‑bit WAV before leveling.
- **PATH issues?** Ensure `~/bin` (or `~/.local/bin`) appears **before** system paths in your shell startup file.

---

## License

MIT © Seven Morris
