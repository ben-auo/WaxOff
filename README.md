# WaxOff — Interactive CLI Stereo Podcast Leveler (FLAC-enabled)

**WaxOff** is the *final step before delivery*. It normalizes stereo podcast audio to **−18 LUFS** (or **−16 LUFS**) via two-pass BS.1770 / EBU R128 (`ffmpeg` `loudnorm`), with a **true-peak ceiling of −1 dBTP**. It’s interactive by default — matching WaxOn’s UX — and can run non-interactively via flags/env.

> Need the *first, intermediate step* before editing? See **[WaxOn](https://github.com/sevmorris/WaxOn)** — it prepares mono channel-0 WAV/FLAC for DAW editing with DC-block, declip, normalization, and limiting.

- Outputs: **24-bit WAV**, **CBR MP3** (128/160/192k), **FLAC** (archival), or combinations
- Atomic hidden-temp writes for safety
- Per-file **spot-check** logs input I/TP
- Installs to **`~/bin`** (or `~/.local/bin`), same location as **WaxOn**

## Install

```bash
brew install ffmpeg
chmod +x waxoff
./install.sh            # copy install to ~/bin (or ~/.local/bin)
./install.sh --dev      # symlink install (development mode)
./install.sh --prefix "$HOME/.dotfiles/bin" --dev   # custom prefix + dev
```

## Interactive usage

```bash
waxoff *.wav
# Prompts for:
#   • Target LUFS (−18/−16)
#   • Output mode (wav | mp3 | both | flac | wav+flac | all)
#   • MP3 bitrate (if mp3 is included)
#   • FLAC compression level (if flac is included)
#   • Sample rate (44100 or 48000)
```

## Non-interactive (flags / env)

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

## Workflow: WaxOn → edit in DAW → WaxOff
1. **WaxOn** to prep mono assets for editing (channel-0, DC-block/declip/limit).
2. **Edit/mix** in your DAW.
3. **WaxOff** to hit final program loudness (−18/−16 LUFS) and create deliverables.

**Back to first step:** [WaxOn on GitHub](https://github.com/sevmorris/WaxOn)

## Uninstall

```bash
./install.sh --uninstall
```

License: MIT
