# Omarchy Dynamic GTK4 Nautilus Theme

A dynamic GTK4 CSS template for the GNOME Nautilus file manager, designed specifically for the **Omarchy** desktop environment.

Whenever you switch your Omarchy theme, this template automatically generates a matching GTK4 stylesheet using your active system palette (background, foreground, accent, and semantic colors) to provide a unified aesthetic across your workflow.

---

## Features

- **Modern Libadwaita Color Blending:** Integrates complete Libadwaita variable definitions using Omarchy's template `mix` engine (e.g. `{{ mix background foreground 6% }}`) for natural surface tints across cards, sidebars, popovers, and dialogs in dark, light, and OLED colorways.
- **Single-Root Typography (85% Scale):** Applies **JetBrains Mono** at an 85% base font scale strictly on the root `window.nautilus-window` selector, ensuring a clean, compact UI without cascading font-scale compounding bugs in child containers.
- **Enhanced Selection & Focus Visibility:** Clear selection highlights across grid, column, list, and sidebar views using alpha-blended accent backgrounds with high-contrast text, custom rubberband selection styling, and distinct focus rings on text entries.
- **Refined Window Chrome:** Eliminates intrusive top bar undershoot shadows and restores a subtle, well-scoped vertical separator between the sidebar and main file view.
- **Automated Validation Suite:** Includes a full Python test suite (`tests/validate_theme.py`) that validates color interpolation math, variable substitution across multiple color palettes, and GTK4 CSS parser syntax using `Gtk.CssProvider`.

---

## Installation

### 1. Copy the Template
Copy `gtk.css.tpl` into your Omarchy user templates directory:

```bash
mkdir -p ~/.config/omarchy/themed
cp gtk.css.tpl ~/.config/omarchy/themed/
```

### 2. Generate the Stylesheet
Cycle or switch your Omarchy theme once (using `Super + Alt + Space` or your preferred shortcut). The Omarchy engine will render the template into:
```
~/.local/state/omarchy/current/theme/gtk.css
```

### 3. Link to GTK4 Configuration
Create a symlink pointing GTK4 to the generated theme:

```bash
mkdir -p ~/.config/gtk-4.0
ln -sf ~/.local/state/omarchy/current/theme/gtk.css ~/.config/gtk-4.0/gtk.css
```

### 4. Restart Nautilus
Restart Nautilus to apply the new stylesheet:

```bash
nautilus -q
```

---

## Omarchy Theme Precedence

> [!NOTE]
> Omarchy prioritizes static files inside individual theme directories over dynamic templates in `~/.config/omarchy/themed/`.
>
> If a theme located in `~/.config/omarchy/themes/<theme-name>/` already contains a static `gtk.css` file, Omarchy will copy that file directly and skip rendering `gtk.css.tpl`. To ensure this dynamic template is used for that theme, remove the static `gtk.css` from the theme's folder.

---

## Development & Testing

This repository includes an automated test harness to verify template integrity and GTK4 CSS compatibility.

Run tests using Python 3:

```bash
python3 tests/validate_theme.py
```

The test suite checks:
- Proper rendering of `mix`, `mix_strip`, `mix_rgb`, and palette variables.
- Verification across Dark, Light, and OLED color palettes.
- Absence of unrendered template tokens.
- Single-root `font-size: 85%` structural rules.
- Direct GTK4 CSS syntax validation via `Gtk.CssProvider` (requires `python-gobject` and GTK4).

---

## Requirements

- **GTK 4.0+** (GNOME Nautilus 43+)
- **Omarchy Desktop Environment**
- **JetBrains Mono** font (`ttf-jetbrains-mono` or system package)
- *(Optional for testing)* `python-gobject` with GTK 4.0
