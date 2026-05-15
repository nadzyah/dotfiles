# dotfiles

Personal configs for sway, waybar, swaylock, i3, and a custom Polish/Deutsch keyboard layout.

## Install

These files live under `$HOME/.config/`. Symlink or copy them:

```sh
ln -s "$PWD/sway"          ~/.config/sway
ln -s "$PWD/waybar"        ~/.config/waybar
ln -s "$PWD/swaylock"      ~/.config/swaylock
ln -s "$PWD/i3"            ~/.config/i3
ln -s "$PWD/xkb"           ~/.config/xkb
ln -s "$PWD/starship.toml" ~/.config/starship.toml
```

Reload sway with `$mod+Shift+c` after install.

## Custom keyboard layout: `pl_de`

Polish layout extended with German umlauts. Set in
`sway/config` as `xkb_layout "pl_de,by"`.

| Keys                | Result                            |
| ------------------- | --------------------------------- |
| `AltGr + y`         | ä                                 |
| `Shift + AltGr + y` | Ä                                 |
| `AltGr + i`         | ö                                 |
| `Shift + AltGr + i` | Ö                                 |
| `AltGr + u`         | ü                                 |
| `Shift + AltGr + u` | Ü                                 |
| `AltGr + t`         | ß (already in standard pl layout) |

All Polish-specific characters (ą, ć, ę, ł, ń, ó, ś, ź, ż) are
preserved

### How it works

- `xkb/symbols/pl_de` extends `pl(basic)` and remaps a few keys at XKB
  level 3/4 (AltGr / Shift+AltGr).
- `xkb/rules/evdev.xml` registers the `pl_de` layout with the XKB
  registry so waybar's `sway/language` module can look it up by
  description (`Polish/Deutsch`) and resolve a short name (`pl/de`)
  and tooltip text.

`libxkbcommon` and the XKB registry (`rxkb`, used by waybar) both
search `~/.config/xkb/` before system paths, so symlinking `xkb/` is
enough — no system files are modified.

### Switching layouts

Caps Lock toggles between `pl_de` and `by` (Belarusian), per
`xkb_options "grp:caps_toggle"` in `sway/config`. The waybar indicator
shows `pl/de` or `by` (tooltip: `Polish/Deutsch` / `Belarusian`).
