# Omarchy Quattro Dynamic Nautilus Theme

A dynamic GTK4 CSS template for the Nautilus file manager, designed specifically for the Omarchy Quattro desktop environment. 

Whenever you switch your Omarchy theme, this template automatically generates a new GTK4 stylesheet to match your system's background, foreground, and accent colors perfectly. It also forces the UI font to **JetBrains Mono** at an 83.33% scale for a cleaner, denser look.

## Installation

1. Clone or download this repository.
2. Copy the template file to your Omarchy templates directory:
   ```bash
   cp gtk.css.tpl ~/.config/omarchy/themed/
   ```
3. Cycle your Omarchy theme once (using `Super + Alt + Space`) to force the engine to generate the CSS file. The output will be placed in `~/.local/state/omarchy/current/theme/gtk.css`.
4. Create a symlink connecting the generated file to your GTK4 configuration:
   ```bash
   mkdir -p ~/.config/gtk-4.0
   ln -sf ~/.local/state/omarchy/current/theme/gtk.css ~/.config/gtk-4.0/gtk.css
   ```
5. Restart Nautilus to apply the changes:
   ```bash
   nautilus -q
   ```

## Notes
* Requires GTK4 (GNOME 43+).
* Ensure you have the `JetBrains Mono` font installed on your system.
