# WaxOff (CLI)
**Fast, safe audio cleanup and reversal** — prepares DAW‑ready dialogue, undoing preprocessing or restoring raw dynamics for post work.

WaxOff complements WaxOn by reversing its effects or cleaning processed audio. It provides clip repair, normalization rollback, and re‑expansion utilities.

---

## 🧩 Install

This project installs by cloning to your home directory and creating a symlink in `~/bin` (or `~/.local/bin`).

### Quick install
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/sevmorris/WaxOff/main/install.sh)"
```

### Verify installation
```bash
waxoff -h
```

If `~/bin` isn’t in your PATH:
```bash
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc
```

### Uninstall (symlink only)
```bash
~/WaxOff/uninstall.sh
```

---

## 🧰 Behavior

- Clones repo to `~/WaxOff`
- Creates symlink `waxoff` in `~/bin` (or `~/.local/bin`)
- Idempotent: can be re‑run to update both repo and symlink

---

## ⚙️ Dependencies

- `bash`, `git`
- `ffmpeg`

---

## 🧾 License

MIT License © Seven Morris
