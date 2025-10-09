# WaxOff — Interactive CLI (Stereo Leveler with WAV/MP3/FLAC)

**WaxOff** is the **final** step before delivery. It takes your edited stereo mix and:
- Runs **two-pass** BS.1770/EBU R128 to **−18 LUFS** (recommended) or **−16 LUFS**  
- True peak set to **−1.0 dBTP**  
- Exports **WAV (24-bit)**, **MP3 (128/160/192 kbps)**, **FLAC (level 0–12)**  
- 44.1 k or 48 k sample rate  
- Hidden temp writes, atomic reveal  
- **Interactive file picker** if started with no filenames  
- **Live console output** mirrored to a log via `tee`

> **Upstream:** Prep your sources first with **[WaxOn](https://github.com/sevmorris/WaxOn)**.

## Requirements

```bash
brew install ffmpeg
```

## Install (user)

```bash
mkdir -p ~/bin && curl -fsSL https://raw.githubusercontent.com/sevmorris/WaxOff/refs/heads/main/waxoff -o ~/bin/waxoff && chmod +x ~/bin/waxoff && case ":$PATH:" in *":$HOME/bin:"*) :;; *) echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc && export PATH="$HOME/bin:$PATH";; esac && echo "Installed waxoff -> ~/bin/waxoff"
```

## Dev setup

```bash
git clone https://github.com/sevmorris/WaxOff.git
cd WaxOff
chmod +x waxoff
./waxoff --help
```

## Quick start

```bash
waxoff
waxoff *.wav
waxoff -t -18 -m all -b 192k --samplerate 48000 mix.wav
```

## Workflow

1. **WaxOn** → clean/prep mono files to −25 LUFS.  
2. **Mix/edit** in DAW.  
3. **WaxOff** → finalize and export deliverables.
