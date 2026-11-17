# GlazeWM & Zebar Configuration (Hyprland + Waybar Style)

A Windows 11 tiling window manager and status bar setup powered by **[GlazeWM v3](https://github.com/glzr-io/glazewm)** and **[Zebar v3](https://github.com/glzr-io/zebar)**, designed to replicate an Arch Linux **Hyprland + Waybar** workflow with TokyoNight/Catppuccin aesthetics.

---

## Directory Structure

```text
~/.glzr/
├── glazewm/
│   └── config.yaml          # GlazeWM v3 window management, workspaces & keybindings
├── zebar/
│   ├── settings.json        # Zebar startup widget configuration
│   └── waybar/              # Custom Waybar-themed topbar widget pack
│       ├── zpack.json       # Widget pack manifest (48px height, all monitors)
│       ├── topbar.html      # React + Zebar providers status bar + inline SVG icons
│       └── styles.css       # TokyoNight/Catppuccin pill styling
└── .gitignore
```

---

## Features

### 1. GlazeWM (Hyprland Workflow)
- **Modifier Key**: Uses `LWin` (`SUPER`) across all window management shortcuts—no `Alt` keybinding collisions with terminal/editor shortcuts (like `Alt+V` in WezTerm).
- **Multi-Monitor Workspace Pinning**:
  - **Monitor 1 (`bind_to_monitor: 0`)**: Workspaces `1` – `5`
  - **Monitor 2 (`bind_to_monitor: 1`)**: Workspaces `6` – `10`
- **Submaps (Binding Modes)**:
  - **`apps` (`SUPER + O`)**: Quick launcher for Chrome, Brave, Firefox, File Explorer, and LocalSend.
  - **`terminal_apps` (`SUPER + T`)**: Quick launcher for WezTerm TUI apps (`yazi`, `btop`, `nvim`).
- **Zero-Gap Tiling**: `0px` inner/outer gaps with a `40px` top outer gap reserved for the Zebar status bar.

### 2. Zebar (`waybar` Custom Pack)
- **Inline SVG Icons**: Crisp, zero-dependency inline vector icons (no broken Nerd Font glyphs).
- **Left Modules**:
  - **Arch Launcher Button**: Left-click opens `wezterm-gui`, Right-click reloads GlazeWM config.
  - **Workspaces Pill**: Displays workspaces for the current monitor + active binding mode (`APPS`, `TERMINAL_APPS`, `RESIZE`) or `PAUSED` badge.
  - **Active Window Pill**: Shows the focused window title.
- **Center Modules**:
  - **Media Player Hub**: Automatically appears when media is playing/paused (`Prev`, `Artist — Title` play/pause toggle, `Next`).
  - **Clock / Calendar Pill**: Displays `hh:mm AM/PM`; click or right-click to toggle the full date (`Day, Month DD, YYYY`).
- **Right Modules**:
  - **CPU & RAM Pills**: Real-time usage stats; click to launch `btop` in WezTerm. Highlights red on high usage (`>85%`).
  - **Network Bandwidth Pill**: Shows Wi-Fi/Ethernet status and live download speed (`󰇚 KB/s` or `MB/s`).
  - **Collapsible System Tray**: Keeps pinned apps (**WhatsApp**, **Discord**) always visible and smoothly expands all other tray icons on hover.
  - **Audio Pill**: Shows volume percentage; click to toggle mute, scroll wheel up/down to adjust volume by `±5%`.
  - **Battery & Power Pill**: Left-click on the power icon locks the workstation; Right-click exits GlazeWM.

---

## Keybindings Reference (`SUPER` = `LWin`)

### Focus & Monitor Navigation
| Shortcut | Action |
| :--- | :--- |
| `SUPER + H / J / K / L` | Focus window Left / Down / Up / Right |
| `SUPER + Left / Down / Up / Right` | Focus window Left / Down / Up / Right |
| `SUPER + ,` / `SUPER + .` | Focus Left / Right Monitor |
| `SUPER + [` / `SUPER + ]` | Focus Previous / Next Workspace on current monitor |
| `SUPER + Tab` | Focus last active workspace |
| `SUPER + 1..9, 0` | Focus Workspace `1` – `10` |

### Move & Resize Windows
| Shortcut | Action |
| :--- | :--- |
| `SUPER + Shift + H / J / K / L` | Move/swap focused window Left / Down / Up / Right |
| `SUPER + Shift + Arrows` | Move/swap focused window Left / Down / Up / Right |
| `SUPER + Shift + ,` / `SUPER + Shift + .` | Move focused window to Left / Right Monitor |
| `SUPER + Shift + 1..9, 0` | Move focused window to Workspace `1` – `10` and follow focus |
| `SUPER + Alt + H / L` | Resize window width `-2%` / `+2%` |
| `SUPER + Alt + K / J` | Resize window height `-2%` / `+2%` |
| `SUPER + Alt + R` or `SUPER + Alt + 0` | Reset window split proportions |

### Window State & WM Control
| Shortcut | Action |
| :--- | :--- |
| `SUPER + Enter` | Launch WezTerm (`wezterm-gui`) |
| `SUPER + Q` | Close focused window |
| `SUPER + F` | Toggle fullscreen |
| `SUPER + Shift + F` | Toggle floating (centered) |
| `SUPER + V` | Toggle tiling direction (horizontal / vertical) |
| `SUPER + M` | Minimize focused window |
| `SUPER + Shift + R` | Reload GlazeWM configuration |
| `SUPER + Shift + W` | Redraw all windows |
| `SUPER + Shift + B` | Restart Zebar status bar |
| `SUPER + Shift + P` | Pause / Unpause GlazeWM |
| `SUPER + Alt + Q` | Quit GlazeWM |

### Application Submaps
- **`SUPER + O` (`apps` mode)** — press `Esc` or `Enter` to cancel:
  - `C` → Google Chrome
  - `B` → Brave Browser
  - `F` → Firefox
  - `T` → Windows File Explorer
  - `L` → LocalSend
- **`SUPER + T` (`terminal_apps` mode)** — press `Esc` or `Enter` to cancel:
  - `L` → `wezterm-gui start yazi`
  - `H` → `wezterm-gui start btop`
  - `N` → `wezterm-gui start nvim`

---

## Customization Tips

- **Pinning More System Tray Icons**:
  Open [`zebar/waybar/topbar.html`](./zebar/waybar/topbar.html) and edit the `PINNED_TRAY_APPS` array:
  ```js
  const PINNED_TRAY_APPS = ['whatsapp', 'discord', 'telegram', 'steam'];
  ```
- **Windows `Win + L` Lock Screen Override**:
  Windows 11 reserves `Win + L` for locking the screen at the OS level. If you want `SUPER + L` to focus right without locking Windows, you can either use `SUPER + Right` or disable `LockWorkstation` in the Windows Registry (`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\System` → `DisableLockWorkstation = 1`).
