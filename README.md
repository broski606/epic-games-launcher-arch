# 🎮 epic-games-launcher
 
![Arch Linux](https://img.shields.io/badge/Arch_Linux-1793D1?logo=archlinux&logoColor=white)
![Status](https://img.shields.io/badge/launcher-Preview-orange)
![License](https://img.shields.io/badge/packaging_license-MIT-green)
 
Unofficial Arch Linux package for the **Epic Games Launcher (Linux Preview)**.
 
It downloads the official `.deb` straight from Epic's servers, verifies its checksum and repackages it for `pacman`. Nothing from Epic is stored or redistributed in this repository.
 
> [!NOTE]
> This project is **not affiliated with or endorsed by Epic Games, Inc.**
> The launcher itself is currently in **Preview**, so expect rough edges.
 
---
 
## ✨ Features
 
- 📦 Installs as a proper `pacman` package (clean install, clean removal)
- 🔒 Checksum-verified download from Epic's official URL
- 🖥️ Desktop entry and icons included, so it shows up in your app menu
- 🔗 Handles the `com.epicgames.launcher://` URL scheme
- 🧹 No post-install scripts, nothing runs as root besides `pacman` itself
## 🧰 Requirements
 
- Arch Linux or an Arch-based distro (Manjaro, EndeavourOS, CachyOS, ...)
- `base-devel` and `git`
```bash
sudo pacman -S --needed base-devel git
```
 
Runtime dependencies (`webkit2gtk-4.1`, `gtk3`, `libayatana-appindicator`, `libsoup3`, ...) are pulled in automatically by `pacman`.
 
## 🚀 Installation
 
```bash
git clone https://github.com/broski606/epic-games-launcher.git
cd epic-games-launcher
makepkg -si
```
 
Then launch **Epic Games Launcher** from your app menu, or run:
 
```bash
EpicGamesLauncher
```
 
## 🔄 Updating
 
Pull the latest packaging changes and rebuild:
 
```bash
cd epic-games-launcher
git pull
makepkg -si
```
 
## 🗑️ Uninstalling
 
```bash
sudo pacman -R epic-games-launcher
```
 
Games you installed through the launcher live in the folder you chose during installation and are **not** removed automatically.
 
## 🩹 Troubleshooting
 
### `One or more files did not pass the validity check`
 
Epic serves the latest launcher build from a URL that never changes, so when they publish a new version the checksum in the `PKGBUILD` no longer matches. This is expected and easy to fix:
 
```bash
# Option A: wait for the PKGBUILD to be updated here (git pull)
 
# Option B: update it yourself
sudo pacman -S --needed pacman-contrib
updpkgsums
makepkg -si
```
 
If `pkgver` is also outdated, you can read the real version from the downloaded file:
 
```bash
bsdtar -xOf EpicGamesLauncher-*.deb control.tar.gz | bsdtar -xOf - ./control | grep Version
```
 
Feel free to open an issue so the package gets updated for everyone.
 
### The launcher doesn't start
 
Run it from a terminal to see the error output:
 
```bash
EpicGamesLauncher
```
 
If a shared library is missing, please open an issue with the output so the dependency list can be fixed.
 
## 🛠️ How it works
 
1. `makepkg` downloads the official `.deb` from Epic and checks its SHA-256.
2. The `data.tar.*` payload is extracted straight into the package directory.
3. Epic's third-party notices are installed to `/usr/share/licenses/`.
4. `pacman` installs the result like any other package.
## 🤝 Contributing
 
Issues and pull requests are welcome, especially for:
 
- Version bumps and checksum updates
- Missing or unnecessary dependencies
- Packaging improvements
## 📜 License
 
The license in this repository (see [`LICENSE`](LICENSE)) covers **only the packaging files** (`PKGBUILD`, this README, etc.).
 
**Epic Games Launcher is proprietary software** owned by Epic Games, Inc. and is downloaded from Epic's official servers at build time. Its use is subject to Epic's own terms.
 
Epic Games, the Epic Games logo and Epic Games Launcher are trademarks of Epic Games, Inc.
