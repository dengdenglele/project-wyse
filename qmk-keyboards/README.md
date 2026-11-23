# How to use QMK keyboard
Use a chromium based browser and open [usevia.app](https://usevia.app/).
Make sure to unplug wireless adapter and connect directly with USB-cable.

1. Settings `cog wheel` symbol
1. Activate `Show Design Tab` slider
1. Design `brush` symbol
1. Load Draft Definition `Load` button
1. Select `.json` file
1. Configure `keyboard` symbol
1. Connect wired keyboard with `Authorize device +`

## Default layers for win/linux and mac
- Sharkoon SGK55W hardware switch `MAC | WIN`:
  - layers 0|1 for `WIN` mode and layers 2|3 for `MAC` mode
- Keychron may use hardware switch `MAC | WIN` differently
  - layers 0|1 for `MAC` mode and layers 2|3 for `WIN` mode

## Tap for ESC and hold for left ctrl (win/linux) or left command (mac)
```
# Windows/Linux
MT(MOD_LCTL,KC_ESC)

# macOS
MT(MOD_LGUI,KC_ESC)
```

## Hold key for layer
Activate (hold) `layer 1` with single key, e.g. with `Fn` key
```
MO(1)
```

## Hold key for layer and tap key for key code
```
# Hold for "LAYER 1", tap for "TAB"
LT(1,KC_TAB)

# Hold for "LAYER 1", tap for "SPACE"
LT(1,KC_SPC)
```

## Clear/reset qmk keyboard
Tested with Sharkoon Skiller SGK55W

```
QK_CLEAR_EEPROM
```

## Keyboard not properly connecting in [usevia.app](usevia.app) on Linux w/ Chrome
- Go to [chrome://device-log](chrome://device-log)
- Give permissions
```
sudo chown $USER:$USER /dev/hidrawX
```


## References
- [QMK docs: Switching and toggling layers](https://docs.qmk.fm/feature_layers#switching-and-toggling-layers)
- [Keychron: How to use VIA to program your keyboard](https://www.keychron.com/blogs/archived/how-to-use-via-to-program-your-keyboard)
- [Keychron: Switching and Toggling Layers: Efficient Keyboard Customization](https://www.keychron.com/blogs/archived/switching-and-toggling-layers-efficient-keyboard-customization)
- [reddit: [QMK] Esc when tapped, Ctrl when held in combination with other keys.](https://www.reddit.com/r/olkb/comments/86ot8k/qmk_esc_when_tapped_ctrl_when_held_in_combination/)
- [GitHub: Fix connection issues with usevia.app on linux](https://github.com/the-via/releases/issues/257#issuecomment-1587048882)
