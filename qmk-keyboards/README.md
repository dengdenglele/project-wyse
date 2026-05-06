# How to use QMK keyboard
Use a chromium based browser and open [usevia.app](https://usevia.app/)

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

## Tap for key command and hold for layer

```
LT(1,KC_TAB)

LT(2,KC_SPC)
```
## Fn key hold for toggle

```
MO(1)
```


## References
- [Switching and toggling layers](https://docs.qmk.fm/feature_layers#switching-and-toggling-layers)
