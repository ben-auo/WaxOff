# WaxOff — Interactive CLI Stereo Podcast Leveler (FLAC-enabled)

**WaxOff** is the **final step before delivery**. It normalizes stereo podcast audio to **−18 LUFS** (or **−16 LUFS**) via two-pass BS.1770 / EBU R128 (`ffmpeg` `loudnorm`), with a **true-peak ceiling of −1 dBTP**. Interactive by default (matching WaxOn’s UX), with flags/env for automation.

> Need the **first, intermediate step** before editing? Use **WaxOn** → https://github.com/sevmorris/WaxOn

- Outputs: **24-bit WAV**, **CBR MP3** (128/160/192k), **FLAC** (archival), or combinations
- Atomic hidden-temp writes; per-file spot-check (input I/TP)
- Installs to **`~/bin`** (fallback **`~/.local/bin`**) — same location as **WaxOn**

---

## Install

**Prereq:** `ffmpeg` in your PATH (macOS: `brew install ffmpeg`).

**One-liner (general install):**
```bash
bash -c 'd=$(mktemp -d); git clone --depth=1 https://github.com/sevmorris/WaxOff "$d" && (cd "$d" && chmod +x waxoff install.sh && ./install.sh) && rm -rf "$d"'
```

**One-liner (dev symlink install):**
```bash
bash -c 'd="$HOME/src/WaxOff"; [ -d "$d/.git" ] || git clone https://github.com/sevmorris/WaxOff "$d"; (cd "$d" && git pull --ff-only && chmod +x waxoff install.sh && ./install.sh --dev)'
```

> The dev one-liner clones (or updates) to `~/src/WaxOff` and symlinks `waxoff` into your user bin dir so edits take effect immediately.

---

## Interactive usage

```bash
waxoff *.wav
# Prompts for:
#   • Target LUFS (−18 / −16)
#   • Output mode (wav | mp3 | both | flac | wav+flac | all)
#   • MP3 bitrate (if mp3 is included)
#   • FLAC compression level (if flac is included)
#   • Sample rate (44100 or 48000)
```

### Example

```bash
waxoff ~/Mixdowns/episode_mix.wav
# → Outputs episode_mix-lev-18LUFS.wav and episode_mix-lev-18LUFS.mp3
```

---

## Non-interactive usage (flags / env)

```bash
waxoff --no-prompt -t -16 -m wav+flac -s 48000 *.aif
# or
PROMPT=0 TARGET_I=-18 OUTMODE=all SAMPLE_RATE=48000 waxoff *.wav
```

### Options

```
  -t, --target <LUFS>      -18 (default) or -16
  -m, --mode <mode>        wav | mp3 | both | flac | wav+flac | all   (default: both)
  -b, --bitrate <rate>     128k | 160k (default) | 192k  (MP3)
  -s, --samplerate <hz>    44100 or 48000
  --flac-level <N>         0..12 compression (default: 8)

  -l, --log <path>         Log file path (default: ~/Library/Logs/waxoff_cli.log)
  --no-prompt              Skip interactive questions
  -q, --quiet              Reduce console output
  -n, --dry-run            Show actions without writing files
```

---

## Updating

To pull the latest version (dev install only):
```bash
cd ~/src/WaxOff && git pull && ./install.sh --dev
```

To reinstall the general version:
```bash
bash -c 'd=$(mktemp -d); git clone --depth=1 https://github.com/sevmorris/WaxOff "$d" && (cd "$d" && ./install.sh) && rm -rf "$d"'
```

---

## Recommended workflow

1) **WaxOn** → prep mono assets for editing (channel-0, DC-block/declipping/limit). → https://github.com/sevmorris/WaxOn  
2) **Edit / mix** in your DAW.  
3) **WaxOff** → finalize program loudness (−18/−16 LUFS) and produce deliverables (WAV/MP3/FLAC).

---

## Uninstall

```bash
./install.sh --uninstall
```

License: MIT
