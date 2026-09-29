# Linux (XKB / Hyprland+Omarchy)

`xkb/symbols/bruno` is the Linux port of this layout (ported from
`bruno-ansi-f.klc`, with a few deliberate differences from the Windows
version based on real muscle-memory testing — see comments in the file).

## Install

```
mkdir -p ~/.config/xkb/symbols
cp linux/xkb/symbols/bruno ~/.config/xkb/symbols/bruno
```

libxkbcommon picks up `~/.config/xkb` automatically (Wayland/Hyprland,
also Sway etc.) — no system-wide install needed.

## Wire it up (Hyprland / Omarchy `~/.config/hypr/input.lua`)

```lua
hl.config({
  input = {
    kb_layout = "bruno",
    kb_model = "abnt2",   -- keep your real hardware model
    kb_variant = "basic",
    kb_options = "",      -- "" = normal CapsLock. Omarchy's default
                          -- ("compose:caps,...") turns CapsLock into a
                          -- Compose key instead — set explicitly if you
                          -- don't want that.
  },
})
```

Applied globally (`hl.config`) this covers every keyboard — laptop and
external — for consistent muscle memory, even though physical keycaps
won't match anymore. Use `hl.device({ name = "...", kb_layout = "bruno",
kb_variant = "basic" })` instead if you want it on one device only
(device names: `hyprctl devices`).

After any change: `hyprctl reload`. Note: `hyprctl reload` alone does NOT
recompile the keymap if only the *file content* changed (not the
layout/variant name) — force it with:

```
hyprctl eval 'hl.config({input={kb_variant=""}})'
hyprctl eval 'hl.config({input={kb_variant="basic"}})'
```
