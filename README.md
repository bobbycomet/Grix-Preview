# Grix a Linux System Companion

> **Griffin Linux project** · GPLv3 · AppImage (coming soon) · v2.5.0

---
<p align="center">
<img width="300" height="300" alt="Grix" src="https://github.com/user-attachments/assets/4dc225b4-21e0-4983-bec2-8a86209a3572" />
</p>

You switched to Linux, or you have been on it for years, and yet there is always *that moment*. Sound stops working after an update. A game crashes on launch for no obvious reason. Your controller connects but does nothing. You Google the error, land on a five-year-old forum thread, try three different commands, and an hour later, you still do not know if you fixed it or just got lucky.

Linux is powerful. It is also unforgiving in ways that have nothing to do with how smart you are. The knowledge required to diagnose a broken PipeWire session, a missing Vulkan ICD, or a Realtek WiFi chip with an out-of-tree driver is specialized, scattered across wikis, and changes with every kernel release. Most people should not have to know any of that just to use their computer.

**Grix exists because that gap is real, and it matters.** It is the tool that watches your system, speaks plainly about what it finds, and handles the fix, so you can get back to whatever you were actually trying to do.

---

Update on Grix – Simplifying for Reliability
Grix is currently under a major review and rewrite. Its core had grown overly complicated, trying to handle too many things across too many different setups. So we've made some focused changes before the first stable release:

- Distro-agnostic features are being removed for now. Grix will focus tightly on Ubuntu-based systems with KDE Plasma (including Griffin Talon Edition and other Ubuntu flavors/spins). This makes it far more reliable and easier to maintain. Other Ubuntu spins and flavors will still benefit significantly from the improvements.

- System health checks are being narrowed down. Other dedicated Griffin tools are now handling broader system optimization and health, so Grix can concentrate on the specific, high-frustration problems that fall outside those tools — the exact things that usually send new users to forums or Reddit.
 
- Process Sentry and Kernel Autotune have been moved into a new unified tool called Game Tune Hub. This keeps performance tuning clean and centralized.

- Postinstaller will now handle environment and app bundle provisioning. Workflow-based automation (e.g., "I'm a gamer/streamer/VTuber") will happen after first boot through simple user choices instead of trying to detect and configure everything automatically.

These changes make Grix lighter, more predictable, and much more reliable, especially across varying kernels and tricky updates like PipeWire. The goal remains exactly the same: 

- a local, transparent companion that spots real issues, explains them plainly, shows you exactly what it will do, asks for your approval, and logs everything so you can learn or undo changes.

- Grix will still serve as the friendly control center that launches the right Griffin tool when needed and guides you through common headaches (hardware quirks, audio glitches, driver situations, etc.) without forcing you to become a terminal expert.

We're taking the time to get this foundation solid because first impressions matter.

Thanks for your patience, this rework will result in a much smoother and more trustworthy experience. The rest of Griffin (FanHub, XKM, Griffin Migrate, Appify, etc.) continues moving forward, and the overall vision of a frustration-free switch from Windows stays fully on track.

## What Is Grix?

Grix is a desktop application for Linux that watches over your system, explains what it finds in plain English, and, when it can, fixes things for you with one click.

Think of it like a friendly dashboard that sits between you and the raw complexity of Linux. When something goes wrong, audio suddenly stops working, a game refuses to launch, the system is running low on disk space, a background service has crashed, Grix spots it, tells you what it means in everyday language, and offers to sort it out. No terminal required.

Under the hood, Grix scans dozens of system properties: running services, audio stack health, GPU drivers, disk space, firmware, network, gaming compatibility layers, streaming tools, VTuber software dependencies, CPU power profiles, backup status, drive health (SMART), system logs, and more. Every issue it finds is ranked by severity — **Error**, **Warning**, or **Info** — so you can see at a glance what needs attention right now versus what is merely worth knowing.

Beyond fixing things, Grix doubles as a learning tool. Each issue card links to a contextual lesson in the built-in "Learn Terminal" section, which teaches you what the underlying command actually does and why. You can act now and learn later, or read before you click; it is entirely up to you.

Grix stores everything locally. There is no telemetry, no cloud account, no data sent anywhere. It reads from the kernel's own files and standard system tools, and it never uses `shell=True` to run commands (a common security pitfall). Privilege escalation for fixes that need it goes through PolicyKit (`pkexec`) where available, falling back to `sudo`.

Grix also uses tray Icons to tell you when a scan happens, when it is asleep, when an issue arises with the level of severity, when everything is fine, and you can right-click to make it quit or sleep.

UI may change from the current look based on the change of Grix.

<img width="300" height="300" alt="GrixFix" src="https://github.com/user-attachments/assets/44bf0d65-b20c-4ce0-8955-fdd9c3ab1216" />
<img width="300" height="300" alt="GrixStudy" src="https://github.com/user-attachments/assets/aa10de42-f782-40e0-afab-90b3ef8af0c3" />
<img width="300" height="300" alt="Grixsleep" src="https://github.com/user-attachments/assets/0e264a0e-1ffe-4510-a182-d06ab6e57d7f" />
<img width="300" height="300" alt="Grixyellow" src="https://github.com/user-attachments/assets/75d04136-2827-449f-b98c-93f5d5191628" />
<img width="300" height="300" alt="Grixred" src="https://github.com/user-attachments/assets/5424b7dc-6e15-4665-83f9-8c3a3a834fe4" />
<img width="300" height="300" alt="Grixgreen" src="https://github.com/user-attachments/assets/7e61a9b4-7f07-4dad-b9d9-39431a8f6ab0" />


---


---

## Hubs — Dedicated Hardware Management Panels (these may get their own tool, or go into Game Tune Hub)

Beyond the general scanner, Grix includes a set of purpose-built **Hubs**: focused panels for hardware categories that are complex enough to deserve their own dedicated interface. Where the scanner surfaces a problem and offers a fix, a Hub gives you the full picture — what hardware you have, what driver is loaded, what your options are, and buttons to act on all of it without leaving the application.

### GPU Hub

The GPU Hub is a full graphics driver manager for NVIDIA, AMD, and Intel GPUs. It reads your actual hardware via PCI IDs and recommends the correct driver, including which NVIDIA generation branch applies to your specific card (current 580.xx, legacy 470.xx for Kepler, or nouveau for unsupported older hardware).

**What it shows:**
- Detected GPU names and PCI IDs for all three vendors
- Current installed driver version and session type (X11 or Wayland)
- Architecture label (Maxwell, Turing, Ada Lovelace, RDNA 3, Intel Arc, etc.)
- Wayland-specific caveats (modeset requirement, GBM/EGL support thresholds)
- Mesa version and ROCm status for AMD
- OpenGL renderer string and Vulkan availability
- While it does help with RTX 50 and RDNA 4, this does not mean upstream compatibility is fixed, those are projects not affiliated with Griffin or Grix

**What you can do with it:**
- Install the NVIDIA open kernel module (recommended for Turing and newer) or the proprietary driver, per distro, with RPM Fusion enabling on Fedora, non-free repo setup on Debian, and AUR handling on Arch
- Install the NVIDIA 470 legacy driver for Kepler cards
- Update NVIDIA drivers and rebuild DKMS modules
- Fix Wayland display parameters (`nvidia-drm.modeset=1`) or X11 tearing via ForceCompositionPipeline
- Install or update Mesa and AMD ROCm
- Install Intel Media Driver (VAAPI) and `intel-gpu-tools`
- Run quick GPU diagnostics directly in the panel (nvidia-smi, glxinfo, vulkaninfo, vainfo)

The hub also includes a plain-English Wayland vs X11 guide explaining which display protocol to use for each GPU family and why.
<img width="1920" height="1080" alt="Screenshot_20260409_125335" src="https://github.com/user-attachments/assets/1c513cc4-ef2b-4498-9bde-5c29ea48ef68" />
<img width="1920" height="1080" alt="Screenshot_20260409_125325" src="https://github.com/user-attachments/assets/5b71762f-62a6-451d-9ddb-9678ed722921" />

---

### WiFi Hub

WiFi on Linux is one of the most frequent pain points, particularly for Realtek and Broadcom chips, which often ship with incomplete or buggy in-kernel drivers. The WiFi Hub reads your actual hardware (both PCI and USB adapters) and matches it against a driver database to tell you exactly what you have, what module is loaded, and what to do if it is not working.

**What it shows:**
- All detected WiFi chips (PCI and USB), matched by vendor/product ID
- Current kernel module status (loaded/installed but not loaded / not installed)
- rfkill status (soft and hard block detection)
- NetworkManager and wpa_supplicant / iwd service state

**What you can do with it:**
- Install the correct driver per detected chip — package installs for standard chips, automated GitHub DKMS clone-and-install for out-of-tree Realtek drivers (rtw89, rtw88, rtl8821ce, 88x2bu, 8814au)
- Install Broadcom proprietary (STA/`wl`) or open-source (`brcmfmac`) drivers with correct blacklisting of conflicting modules
- Install Intel `iwlwifi` firmware or MediaTek firmware packages
- Reload individual modules, blacklist conflicting ones
- Run `rfkill unblock wifi` and restart NetworkManager from the panel
- Access a built-in WiFi diagnostics reference (lspci, lsusb, iwconfig, rfkill, nmcli, dmesg)

For Realtek chips, especially, the hub automates the otherwise manual process of cloning a community driver repository, running DKMS install, loading the module, and persisting it at boot.
<img width="1920" height="1080" alt="Screenshot_20260409_125424" src="https://github.com/user-attachments/assets/3c10db1e-49a6-4448-8326-13db720a4a7d" />

---

### Controller Hub

Getting a controller working on Linux, particularly Xbox controllers, means choosing the right kernel driver from several competing options that cannot safely coexist. The Controller Hub manages this for you: it shows what is installed, explains the differences between the drivers, and handles installation with automatic blacklisting of anything that would conflict.

**Supported drivers:**

- **xpadneo** — The recommended Bluetooth driver for Xbox One, Xbox Elite Series 2, and Xbox Series X\|S controllers. Adds proper trigger rumble, accurate axis ranges, battery reporting, and support for 8BitDo, GuliKit KingKong, and GameSir controllers. Bluetooth only; use xone for USB.
- **xone + xpad-noone** — For USB and Xbox Wireless Dongle connections. xone replaces the built-in `xpad` driver for Xbox One/Series hardware; xpad-noone is its companion for older Xbox/Xbox 360 controllers that need legacy `xpad` support alongside xone. These two are designed to run as a pair.
- **xpad** — The upstream kernel legacy driver (original Xbox, Xbox 360, Xbox 360 Wireless). The fallback option when xone is not appropriate.
- **hid-tmff2** — Force feedback driver for Thrustmaster racing wheels (T300RS, T248, TX, T128, T598, TS-PC, TS-XW). Does not conflict with any Xbox driver and can be installed alongside any of the above.
- These are third-part drivers, those projects are handled outside of Griffin and Grix by different maintainers.

**What it shows:**
- Live status for each driver (active/installed but not loaded/not installed)
- Which modules are currently loaded
- Which blacklist entries are in effect

**What you can do with it:**
- Install any driver with one click — including DKMS build and module loading
- Switch between drivers with automatic blacklisting of the outgoing one
- Manually blacklist or un-blacklist individual modules
- Configure xpadneo quirks for third-party controllers (8BitDo Nintendo layout swap, GameSir trigger rumble disable, GuliKit MAC-based flags) via an editable config file and one-click driver reload
- Access a full pairing and connection guide for Bluetooth (bluetoothctl flow), USB, and Xbox Wireless Dongle connections
- Run controller detection checks (`ls /dev/input/js*`, `jstest`, `evtest`, `fftest`) directly from the panel

<img width="1920" height="1080" alt="Screenshot_20260409_125244" src="https://github.com/user-attachments/assets/72d79fec-0809-4102-afc6-9285d8f73629" />

---

## CPU Hub in progress

---

## Who Is Grix *Not* For?

**Users with highly non-standard or custom workflows.** Grix is built around common, well-documented use cases. If you have a heavily customized audio routing pipeline, a bespoke kernel build, a non-standard display manager, or niche hardware with out-of-tree drivers, Grix may not know how to evaluate your setup correctly. It will still catch many general issues, but you should not expect it to reason about edge cases it was never designed for. The plugin system (see below) exists partly to address this over time.

**Enterprise and managed environments.** Some of Grix's checks are useful in any context: disk space, service health, drive SMART status, but Grix is not an IT management platform. It does not understand GPO-equivalents, centrally managed software repositories, mandatory access control policies (SELinux, AppArmor in enforcing mode), or corporate proxy configurations. If you are managing a fleet of machines or working within a locked-down enterprise image, Grix will help with general hygiene, but it is not a replacement for purpose-built IT tools.

**Users who prefer the terminal.** If you are comfortable with `systemctl`, `journalctl`, `dmesg`, `pacman`, and friends, Grix does not add much that you cannot do yourself. It is a convenience tool for users who do not want to interact with those tools directly, not a power-user interface over them.

**Purists.** Grix makes opinionated decisions about what a healthy Linux desktop looks like. It may flag the absence of tools you intentionally do not have, or suggest fixes that do not align with your philosophy. You can dismiss individual issues and permanently mark them resolved, or disable entire check categories in Settings, but if you prefer zero automation and zero suggestions, Grix is not for you.

---

## Grix Covers a Lot, But Not Everything

Grix is a broad-coverage companion, not a specialist tool. It is very good at catching the common things that go wrong on a Linux desktop across a wide range of distros and use cases. It is not a replacement for dedicated tools when you need to go deep: `smartmontools` for forensic drive analysis, `perf` for CPU profiling, Wireshark for network forensics, or a full observability stack for servers.

That is why Grix has a **plugin system**. Third parties, and you, can write Python plugins that add custom checks to the Grix scanner without modifying Grix itself. Drop a `.py` file into `~/.local/share/grix/plugins/` and it is loaded automatically on next launch. Plugins register themselves with `register_plugin()` and return standard `Issue` objects that appear in the main scan UI exactly like built-in checks. This makes Grix extensible for niche workflows without bloating the core.

---

## Licensing and Branding

Grix is released under the **GNU General Public License v3 (GPLv3)**. The GPLv3 was chosen specifically because the name **Grix** and all associated icons and visual identity are part of the **Griffin Linux** branding. The copyleft terms of GPLv3 ensure that if anyone distributes a modified version of Grix, they must do so under the same license and cannot rebrand it as a proprietary product built on Griffin Linux's work.

Plugins you write for your own use are not affected by this; the plugin API is intentionally simple and does not create a derivative work of Grix itself under normal use.

---

## Distribution

Grix will be distributed as an **AppImage** when released. An AppImage is a single self-contained file that runs on any modern Linux distribution without installation. Download it, make it executable (`chmod +x Grix-*.AppImage`), and run it. No package manager, no root, no system changes required for the application itself.

AppImage requires FUSE to mount the image at runtime. Grix itself checks for both libfuse2 and libfuse3, so if your system is missing one, Grix will tell you, and offer to install it.

---

## Technical Reference

### Requirements

- Python 3.10+
- PyQt6
- A systemd-based Linux distribution (Debian/Ubuntu)
- KDE
- JetBrains Mono font (optional but recommended; used for terminal-style detail views)

### Supported Distros

Grix detects the running distro via `/etc/os-release` and adapts all install commands and fix steps accordingly. Supported families:

| Family | Detection | Package Manager |
|---|---|---|
| Debian/Ubuntu and derivatives | `apt` + `dpkg` present | `apt` |

---

### Security Notes

- Grix never uses `shell=True` for subprocess calls. All commands are passed as lists to prevent shell injection.
- Privilege escalation uses `pkexec` (PolicyKit, graphical prompt) when available, falling back to `sudo`. It never stores or caches credentials.
- All file reads use Python's standard library directly from `/proc`, `/sys`, and `/etc`. No third-party scanning dependencies.
- The plugin system loads arbitrary Python files from a user-controlled directory. Only install plugins you trust.

---

*Grix is part of the Griffin Linux project. The name Grix, the Griffin Linux name, and associated icons are protected under the GPLv3 to preserve the integrity of the branding in all distributed versions.*
