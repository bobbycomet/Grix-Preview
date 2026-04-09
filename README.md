# Grix a Linux System Companion

> **Griffin Linux project** · GPLv3 · AppImage (coming soon) · v2.5.0

---
<p align="center">
<img width="300" height="300" alt="Grix" src="https://github.com/user-attachments/assets/4dc225b4-21e0-4983-bec2-8a86209a3572" />
</p>

You switched to Linux, or you have been on it for years, and yet there is always *that moment*. Sound stops working after an update. A game crashes on launch for no obvious reason. Your controller connects but does nothing. You Google the error, land on a five-year-old forum thread, try three different commands, and an hour later, you still do not know if you fixed it or just got lucky.

Linux is powerful. It is also unforgiving in ways that have nothing to do with how smart you are. The knowledge required to diagnose a broken PipeWire session, a missing Vulkan ICD, or a Realtek WiFi chip with an out-of-tree driver is specialized, scattered across wikis, and changes with every kernel release. Most people should not have to know any of that just to use their computer.

**Grix exists because that gap is real, and it matters.** It is the tool that watches your system, speaks plainly about what it finds, and handles the fix — so you can get back to whatever you were actually trying to do.

---

## What Is Grix?

Grix is a desktop application for Linux that watches over your system, explains what it finds in plain English, and, when it can, fixes things for you with one click.

Think of it like a friendly dashboard that sits between you and the raw complexity of Linux. When something goes wrong, audio suddenly stops working, a game refuses to launch, the system is running low on disk space, a background service has crashed, Grix spots it, tells you what it means in everyday language, and offers to sort it out. No terminal required.

Under the hood, Grix scans dozens of system properties: running services, audio stack health, GPU drivers, disk space, firmware, network, gaming compatibility layers, streaming tools, VTuber software dependencies, CPU power profiles, backup status, drive health (SMART), system logs, and more. Every issue it finds is ranked by severity — **Error**, **Warning**, or **Info** — so you can see at a glance what needs attention right now versus what is merely worth knowing.

Beyond fixing things, Grix doubles as a learning tool. Each issue card links to a contextual lesson in the built-in "Learn Terminal" section, which teaches you what the underlying command actually does and why. You can act now and learn later, or read before you click; it is entirely up to you.

Grix stores everything locally. There is no telemetry, no cloud account, no data sent anywhere. It reads from the kernel's own files and standard system tools, and it never uses `shell=True` to run commands (a common security pitfall). Privilege escalation for fixes that need it goes through PolicyKit (`pkexec`) where available, falling back to `sudo`.

Grix also uses tray Icons to tell you when a scan happens, when it is asleep, when an issue arises with the level of severity, when everything is fine, and you can right-click to make it quit or sleep.


<img width="300" height="300" alt="GrixFix" src="https://github.com/user-attachments/assets/44bf0d65-b20c-4ce0-8955-fdd9c3ab1216" />
<img width="300" height="300" alt="GrixStudy" src="https://github.com/user-attachments/assets/aa10de42-f782-40e0-afab-90b3ef8af0c3" />
<img width="300" height="300" alt="Grixsleep" src="https://github.com/user-attachments/assets/0e264a0e-1ffe-4510-a182-d06ab6e57d7f" />
<img width="300" height="300" alt="Grixyellow" src="https://github.com/user-attachments/assets/75d04136-2827-449f-b98c-93f5d5191628" />
<img width="300" height="300" alt="Grixred" src="https://github.com/user-attachments/assets/5424b7dc-6e15-4665-83f9-8c3a3a834fe4" />
<img width="300" height="300" alt="Grixgreen" src="https://github.com/user-attachments/assets/7e61a9b4-7f07-4dad-b9d9-39431a8f6ab0" />



---

## What Grix Covers

Grix runs a comprehensive scan across the following areas, each of which can be toggled on or off in Settings:

**Core system**
- Package manager health and pending updates (apt, pacman, dnf, zypper) NOT a replacement for the package manager
- Systemd service failures (NetworkManager, Bluetooth, PipeWire, and more)
- Audio stack — PipeWire, PulseAudio, missing sinks, crashed audio servers
- Bluetooth — firmware gaps, kernel log errors
- Disk space and inode usage across all mounted partitions
- Firmware blobs — missing or failed kernel firmware loads
- GPU drivers and DKMS module status
- Display stack — Wayland vs X11, compositor detection
- Flatpak and Snap runtime health
- Network connectivity and DNS
- Thermal — overheating CPUs, missing cooling drivers

**Hardware and low-level**
- SMART drive health (early warning of failing drives)
- Machine Check Exception (MCE) and EDAC memory errors
- USB errors from the kernel log
- CPU power governor and throttling
- Microcode updates (Intel and AMD)
- OOM events, swap pressure, and zram configuration
- GRUB staleness, initramfs freshness, EFI boot entries

**Gaming**
- Steam and Proton installation
- Vulkan ICD drivers (per GPU: NVIDIA, AMD, Intel)
- 32-bit/multilib support for older titles
- GameMode, MangoHud, Gamescope
- CPU governor suitability for gaming
- Wine, Wine-Staging, GE-Proton, vkd3d-proton, Bottles
- FUSE (libfuse2 and libfuse3) for AppImages and game launchers
- Controller support — including third-party controllers via Steam Input, ds4drv, xpadneo, and others
- HDR availability and Gamescope HDR mode

**Streaming and content creation**
- OBS Studio (native and Flatpak), required plugins, V4L2 (virtual camera)
- PipeWire screen capture readiness for Wayland
- Video encoding hardware acceleration (VAAPI, NVENC, AMD AMF)
- DaVinci Resolve dependencies and GPU acceleration prerequisites
- Kdenlive, Blender, Inkscape, GIMP readiness checks

**VTuber**
- VSeeFace, VNyan, and related runtime dependencies
- Wine environment for Windows-only VTuber software
- Virtual camera support (V4L2loopback) for avatar output
- PulseAudio/PipeWire virtual sinks for audio routing

**Production/office**
- LibreOffice installation and font coverage
- PDF tooling
- Backup health — Timeshift snapshots, BorgBackup, Restic freshness

**Maintenance**
- Systemd timer and cron job failures
- User group membership (audio, video, input, gamepad, etc.)
- Fix history log (30-day rolling record of every applied fix)
<img width="1920" height="1080" alt="Screenshot_20260409_125150" src="https://github.com/user-attachments/assets/43ac2dbf-7820-4897-b29e-5ae41bcf66ac" />
<img width="1920" height="1080" alt="Screenshot_20260409_125536" src="https://github.com/user-attachments/assets/62956602-828d-4c3b-8e50-43e868884523" />
<img width="1920" height="1080" alt="Screenshot_20260409_125602" src="https://github.com/user-attachments/assets/a07a438d-764a-402f-abb2-033cb86008c6" />
<img width="1920" height="1080" alt="Screenshot_20260409_125635" src="https://github.com/user-attachments/assets/210c80c1-106b-4f70-b1f4-6ca16b31fafc" />

---

## Hubs — Dedicated Hardware Management Panels

Beyond the general scanner, Grix includes a set of purpose-built **Hubs**: focused panels for hardware categories that are complex enough to deserve their own dedicated interface. Where the scanner surfaces a problem and offers a fix, a Hub gives you the full picture — what hardware you have, what driver is loaded, what your options are, and buttons to act on all of it without leaving the application.

### GPU Hub

The GPU Hub is a full graphics driver manager for NVIDIA, AMD, and Intel GPUs. It reads your actual hardware via PCI IDs and recommends the correct driver — including which NVIDIA generation branch applies to your specific card (current 580.xx, legacy 470.xx for Kepler, or nouveau for unsupported older hardware).

**What it shows:**
- Detected GPU names and PCI IDs for all three vendors
- Current installed driver version and session type (X11 or Wayland)
- Architecture label (Maxwell, Turing, Ada Lovelace, RDNA 3, Intel Arc, etc.)
- Wayland-specific caveats (modeset requirement, GBM/EGL support thresholds)
- Mesa version and ROCm status for AMD
- OpenGL renderer string and Vulkan availability
- While it does help with RTX 50 and RDNA 4, this does not mean upstream compatibility is fixed

**What you can do with it:**
- Install the NVIDIA open kernel module (recommended for Turing and newer) or the proprietary driver, per distro — with RPM Fusion enabling on Fedora, non-free repo setup on Debian, and AUR handling on Arch
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
- Current kernel module status (loaded / installed but not loaded / not installed)
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

**What it shows:**
- Live status for each driver (active / installed but not loaded / not installed)
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

## Who Is Grix For?

### Windows switchers

If you have recently moved from Windows, Linux can feel like a different world. Device drivers, audio servers, package managers, and desktop environments, the vocabulary alone is unfamiliar. Grix is designed to remove that friction. It explains issues in the same plain language you would use to describe a problem to a friend, and its one-click fixes handle the terminal commands behind the scenes. The built-in lesson system is there when you are ready to understand what is actually happening; you are never forced to read it just to fix something.

### General everyday users

You want your computer to work. You do not particularly care how. Grix lets you stay in that mindset. Open it after an update, after something feels off, or just occasionally to confirm everything is healthy. It works quietly, surfaces real problems, and stays out of your way the rest of the time.

### Gamers

Gaming on Linux has come a long way, with Steam, Proton, Wine, Lutris, Heroic, but the ecosystem still has sharp edges. Missing Vulkan drivers, broken 32-bit support, the wrong CPU governor, a missing GameMode install, an AppImage that fails silently because libfuse2 is absent: Grix knows to look for all of these and more. It also checks HDR readiness and Gamescope, checks your controller configuration (including third-party controllers like DualSense, Xbox via xpadneo, and generic USB HID devices), and surfaces Steam Input quirks. If a game is misbehaving and you do not know why, running a Grix scan is a fast first step.

### Streamers

OBS, virtual cameras, screen capture under Wayland, hardware video encoding, and streaming on Linux have specific requirements that are easy to miss. Grix checks whether OBS is installed and functional, whether V4L2 is available for a virtual camera, whether the relevant PipeWire capture portal is working, and whether your GPU supports NVENC, VAAPI, or AMD AMF for encoding. It also checks for common OBS plugin gaps.

### VTubers

Running VTuber software on Linux often means running Windows-native apps through Wine, routing audio through virtual PulseAudio sinks, and piping video through V4L2loopback. Each of those layers can break quietly. Grix checks the whole chain: the Wine environment, the virtual audio sink, V4L2loopback module availability, and the known runtime dependencies for popular VTuber applications.

### Production users (office and document work)

If your day is spreadsheets, documents, PDFs, and email, Grix makes sure the tools that support that workflow are healthy, including LibreOffice installation and font coverage, PDF utilities, backup snapshot freshness, and general system stability.

### Users who are tired of the terminal for everything

The terminal is powerful, but not everyone wants to learn thirty commands just to find out why their speakers stopped working. Grix is for the user who knows they need *something* done but does not want to research which command, in which syntax, with which flags, on which distro. Grix figures that out and asks before acting.

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

AppImage requires FUSE to mount the image at runtime. Grix itself checks for both libfuse2 and libfuse3, so if your system is missing one, Grix will tell you — and offer to install it.

---

## Technical Reference

### Requirements

- Python 3.10+
- PyQt6
- A systemd-based Linux distribution (Debian/Ubuntu, Arch/Manjaro/EndeavourOS, Fedora, openSUSE, SteamOS/Bazzite, and derivatives)
- JetBrains Mono font (optional but recommended; used for terminal-style detail views)

### Supported Distros

Grix detects the running distro via `/etc/os-release` and adapts all install commands and fix steps accordingly. Supported families:

| Family | Detection | Package Manager |
|---|---|---|
| Debian / Ubuntu and derivatives | `apt` + `dpkg` present | `apt` |
| Arch / Manjaro / EndeavourOS | `pacman` present | `pacman`, AUR (yay, paru, trizen, pikaur) |
| Fedora and RPM-based | `dnf` present | `dnf`, RPM Fusion, COPR |
| openSUSE | `zypper` present | `zypper` |
| SteamOS/Bazzite | `ID=steamos` or `ID=bazzite` in os-release | `rpm-ostree`, Flatpak |
| Immutable (Silverblue, Kinoite, MicroOS) | `rpm-ostree` or `bootc` present | `rpm-ostree` + Flatpak |

On immutable distros, Grix automatically prefers Flatpak installs and `rpm-ostree` overlays over traditional package manager commands.

### Running Grix

**GUI mode (default)**

```
python3 grix.py
# or, once installed as AppImage:
./Grix.AppImage
```

**CLI mode**

Append `--cli` to enter headless mode, which runs checks without a graphical interface. Useful in scripts, SSH sessions, or for automation.

```
python3 grix.py --cli <subcommand> [options]
```

**Guardian daemon mode**

```
python3 grix.py --guardian
```

The Guardian runs as a background process, performing pulse scans on a configurable interval and optionally applying safe fixes automatically. See the Guardian section below for full details.

---

### CLI Reference

#### `grix --cli scan`

Run a full system scan and print results to stdout.

```
grix --cli scan [--format text|json] [--pulse] [--dry-run] [--simulate-distro DISTRO]
```

| Flag | Description |
|---|---|
| `--format text` | Human-readable output (default) |
| `--format json` | Machine-readable JSON — includes distro, kernel, scan time, issue list, and summary counts |
| `--pulse` | Fast pulse scan: checks services, packages, GPU, and audio only (skips disk, firmware, network, thermal) |
| `--dry-run` | Show what fix commands would be run without executing them |
| `--simulate-distro DISTRO` | Set `GRIX_SIMULATE_DISTRO` environment variable to simulate a different distro for testing |

**JSON output schema:**

```
{
  "distro": "Ubuntu 24.04",
  "kernel": "6.8.0-45-generic",
  "scan_time": "2025-04-09T14:32:00",
  "pulse": false,
  "dry_run": false,
  "issues": [
    {
      "id": "pipewire_not_running",
      "title": "PipeWire audio server is not running",
      "severity": "error",
      "category": "Audio",
      "description": "...",
      "trust_level": "never_auto",
      "fix_steps": [{"label": "Start PipeWire", "cmd": "systemctl --user start pipewire"}],
      "suggested_fix": ""
    }
  ],
  "summary": {
    "total": 3,
    "errors": 1,
    "warnings": 1,
    "info": 1
  }
}
```

#### `grix --cli fix`

Apply an automated fix for a specific issue by its ID. Issue IDs are shown in `scan` output and in JSON.

```
grix --cli fix --issue-id ISSUE_ID [--yes] [--dry-run]
```

| Flag | Description |
|---|---|
| `--issue-id ID` | The issue ID to fix (required) |
| `--yes` | Skip the confirmation prompt and apply immediately |
| `--dry-run` | Print the fix commands without running them |

Without `--yes`, Grix prints the fix title, trust level, and each step command, then asks for confirmation before proceeding.

**Example:**

```
# See what is wrong
grix --cli scan

# Apply a fix non-interactively
grix --cli fix --issue-id libfuse2_missing --yes

# Preview what the fix would do without running it
grix --cli fix --issue-id gaming_cpu_governor --dry-run
```

#### `grix --cli doctor`

A quick system health summary modelled after Windows' `sfc /scannow` or `apt doctor`. Prints distro, kernel, VM status, immutable OS detection, battery level (if applicable), key service states, and a brief issue count from a pulse scan.

```bash
grix --cli doctor
```

```
══ Grix Doctor ══════════════════════════════════════════
  Distro  : Fedora Linux 40
  Kernel  : 6.9.3-200.fc40.x86_64
  VM      : no
  Immutable: no
  Battery : 87% (Discharging)

  Services:
    ✓ NetworkManager: active
    ✓ bluetooth: active
    ✓ pipewire: active

  Issues  : 0 error(s), 1 warning(s), 2 info
  Run 'grix --cli scan' for details.
══════════════════════════════════════════════════════════
```

---

### The Issue Model

Every finding Grix produces is an `Issue` object. The key fields:

| Field | Description |
|---|---|
| `id` | Stable string identifier (e.g. `vulkan_icd_missing`, `disk_full_/home`) |
| `title` | Short plain-English headline |
| `description` | Full explanation of what is wrong and why it matters |
| `severity` | `error`, `warning`, or `info` |
| `category` | Grouping label (Audio, Gaming, Disk, Firmware, etc.) |
| `fix_steps` | Ordered list of `(label, command)` tuples to apply the fix |
| `trust_level` | Controls Guardian auto-fix behaviour (see below) |
| `suggested_fix` | Human-readable hint shown if an automated fix step fails |
| `learn_section` | Links to the relevant lesson in the built-in Learn Terminal |

**Trust levels:**

| Level | Meaning | Guardian Balanced | Guardian Aggressive |
|---|---|---|---|
| `always_safe` | Low-risk, easily reversible (e.g. restart a service) | Auto-applied | Auto-applied |
| `requires_confirm` | Moderate impact (e.g. install a package) | Notify only | Auto-applied |
| `never_auto` | High impact or irreversible (e.g. OS-layer change, reboot needed) | Notify only | Notify only |

---

### The Guardian (Background Service)

The Guardian is Grix's optional background daemon. When enabled, it wakes on a configurable interval, runs a pulse scan, and acts based on the configured **maintenance policy**:

| Policy | Behaviour |
|---|---|
| `conservative` | Scan only — log findings, never act |
| `balanced` (default) | Auto-apply `always_safe` fixes; send desktop notifications for everything else |
| `aggressive` | Auto-apply `always_safe` and `requires_confirm` fixes; notify for `never_auto` issues |

The Guardian skips scans when the battery is below 15% to avoid draining a laptop. It can also be configured to run a targeted scan immediately after package updates (`guardian_post_update`).

Desktop notifications are sent via `notify-send` and appear in the standard system notification area.

Guardian settings are stored in `~/.local/share/grix/settings.json` and can be edited from the Settings tab in the GUI or directly in the file.

---

### The Plugin System

Grix exposes a stable plugin API for extending the scanner with custom checks. Plugins are plain Python files placed in `~/.local/share/grix/plugins/`. Every `.py` file in that directory is loaded automatically when Grix starts (GUI, CLI, and Guardian modes all load plugins).

**Minimal plugin example:**

```
# ~/.local/share/grix/plugins/my_check.py

from grix import register_plugin, Issue

def my_check(settings: dict) -> list:
    issues = []
    # ... your logic here ...
    if something_wrong:
        issues.append(Issue(
            title="My custom issue",
            description="Something is not right with my custom setup.",
            severity=Issue.WARNING,
            category="Custom",
            fix_steps=[("Fix it", ["systemctl", "restart", "my-service"])],
            issue_id="my_custom_issue",
            trust_level=Issue.TRUST_CONFIRM,
        ))
    return issues

register_plugin("com.example.mycheck", "My Custom Check", my_check)
```

Plugins receive the current user settings dict so they can respect the same toggle flags as built-in checks. They return a list of `Issue` objects, which appear in the main scan UI alongside built-in results. Plugin load errors are recorded in the debug log and never crash the application.

---

### Data Storage

All Grix data lives under `~/.local/share/grix/`:

| Path | Contents |
|---|---|
| `settings.json` | User preferences and check toggles |
| `trusted.json` | Issues permanently marked as resolved |
| `logs/fix_history.jsonl` | Rolling 30-day log of every applied fix (JSONL format) |
| `debug.log` | Timestamped diagnostic log (plugin loads, Guardian pulse results, fix outcomes) |
| `plugins/` | User-installed plugin `.py` files |

No data is written outside this directory. No network connections are made.

---

### Settings Reference

The following keys are recognised in `settings.json`. All are booleans unless noted.

| Key | Default | Description |
|---|---|---|
| `gaming_checks` | `true` | Gaming-specific checks (Vulkan, Proton, GameMode, controllers, etc.) |
| `streaming_checks` | `true` | OBS, virtual camera, encoding hardware |
| `vtuber_checks` | `true` | VTuber software dependencies and audio routing |
| `production_checks` | `true` | LibreOffice, PDF tools, backup health |
| `content_creation_checks` | `true` | DaVinci Resolve, Kdenlive, Blender, hardware encoding |
| `advanced_hardware_checks` | `true` | SMART drive health, MCE/EDAC, USB kernel errors |
| `memory_checks` | `true` | OOM events, swap pressure, zram |
| `boot_checks` | `true` | GRUB staleness, initramfs, EFI entries |
| `timer_checks` | `true` | Systemd timer and cron job failures |
| `cpu_power_checks` | `true` | CPU governor, throttling, microcode |
| `permission_checks` | `true` | User group membership |
| `backup_checks` | `true` | Timeshift, BorgBackup, Restic |
| `maintenance_policy` | `"balanced"` | Guardian policy: `"aggressive"`, `"balanced"`, `"conservative"` |
| `guardian_enabled` | `false` | Enable the Guardian background daemon |
| `guardian_interval_min` | `60` | Minutes between Guardian pulse scans |
| `guardian_post_update` | `true` | Run targeted scan after package updates |

---

### Environment Variables

| Variable | Description |
|---|---|
| `GRIX_SIMULATE_DISTRO` | Override distro detection for testing. Set to `ubuntu`, `arch`, `fedora`, or `opensuse`. |

---

### Security Notes

- Grix never uses `shell=True` for subprocess calls. All commands are passed as lists to prevent shell injection.
- Privilege escalation uses `pkexec` (PolicyKit, graphical prompt) when available, falling back to `sudo`. It never stores or caches credentials.
- All file reads use Python's standard library directly from `/proc`, `/sys`, and `/etc`. No third-party scanning dependencies.
- The plugin system loads arbitrary Python files from a user-controlled directory. Only install plugins you trust.

---

*Grix is part of the Griffin Linux project. The name Grix, the Griffin Linux name, and associated icons are protected under the GPLv3 to preserve the integrity of the branding in all distributed versions.*
