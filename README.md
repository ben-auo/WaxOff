# WaxOff — Final Mix Loudness Leveler (WAV / MP3 / FLAC)

**Purpose:** WaxOff finalizes stereo mixes to consistent broadcast/podcast loudness using transparent two‑pass **EBU R128 / BS.1770** normalization and a **−1 dBTP** safety ceiling, then exports **WAV, MP3, and/or FLAC**. Ideal as the last step before delivery.

> For pre‑mix prep (mono WAV with limiter‑only chain for editing), see **[WaxOn](https://github.com/sevmorris/WaxOn)**.

---

## Features

- Two‑pass `loudnorm` to **−18 LUFS** (default) or **−16 LUFS**
- True‑peak safety ceiling **−1 dBTP**
- Deliverables: **WAV 24‑bit**, **CBR MP3** (128/160/192 kbps), **FLAC** (level 0–12)
- Choose sample rate **44.1 kHz (default)** or 48 kHz
- **Interactive prompts** (or scriptable with flags/env)
- **macOS file picker** when launched without args
- **Atomic writes** with hidden temps
- Minimal deps: `bash`, `ffmpeg`

---

## Install (one‑liner)

Installs to `~/WaxOff` and symlinks `waxoff` into `~/bin` (or `~/.local/bin`).

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/sevmorris/WaxOff/main/install.sh)"
```

> Ensure `~/bin` is on your `PATH` (see WaxOn README for examples).

---

## Usage

### Interactive

```bash
waxoff *.wav
```

Prompts for:

- Target loudness: **−18** or **−16 LUFS**
- Output mode: `wav` | `mp3` | `both` | `flac` | `wav+flac` | `all`
- MP3 bitrate: 128k, **160k**, 192k
- FLAC compression: **8** by default (0–12)
- Sample rate: **44.1 kHz** or 48 kHz

### Non‑interactive

```bash
# flags
waxoff --no-prompt -t -18 -m wav+flac -b 192k -s 48000 *.aif

# or via env
PROMPT=0 TARGET_I=-18 OUTMODE=all SAMPLE_RATE=48000 MP3_BITRATE=192k waxoff *.wav
```

#### Common flags

- `-t, --target <LUFS>`: `-18` (default) or `-16`
- `-m, --mode <mode>`: `wav | mp3 | both | flac | wav+flac | all` (default `both`)
- `-b, --bitrate <rate>`: `128k | 160k | 192k` (MP3 CBR; default `160k`)
- `-s, --samplerate <hz>`: `44100 | 48000` (default `44100`)
- `--flac-level <0..12>`: FLAC compression level (default `8`)
- `-l, --log <path>`: log file path (default `~/Library/Logs/waxoff_cli.log`)
- `--no-prompt`, `-q`, `-n`: as in WaxOn

---

## Workflow

1. Mix in DAW → bounce stereo WAV (24‑bit recommended)
2. **WaxOff** → pick target loudness and deliverables
3. Deliver masters (WAV/MP3/FLAC)

---

## About (for GitHub sidebar)

A command‑line **finisher** for delivery‑ready podcast masters. Performs transparent two‑pass loudness normalization to **−18 or −16 LUFS** with a **−1 dBTP** ceiling, then exports **WAV, MP3, and/or FLAC**—consistent, headroom‑safe outputs with interactive prompts and atomic writes.

---

## License

MIT © Seven Morris
