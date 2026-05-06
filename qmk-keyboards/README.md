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

## Tap for ESC and hold for left ctrl

```
MT(MOD_LCTL,KC_ESC)
```

## Hold key for layer
Activate (hold) `layer 1` with single key, e.g. with `Fn` key

```
MO(1)
```

## Hold key for layer and tap key for key code
Activate (hold/tap) `layer 2/tab` and `layer 3/space`

```
LT(2,KC_TAB)

LT(3,KC_SPC)
```

## Clear/reset qmk keyboard
Tested with Sharkoon Skiller SGK55W

```
QK_CLEAR_EEPROM
```


## References
- [Switching and toggling layers](https://docs.qmk.fm/feature_layers#switching-and-toggling-layers)
- [reddit: [QMK] Esc when tapped, Ctrl when held in combination with other keys.](https://www.reddit.com/r/olkb/comments/86ot8k/qmk_esc_when_tapped_ctrl_when_held_in_combination/)
