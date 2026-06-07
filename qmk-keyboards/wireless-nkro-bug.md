# Wireless Keyboard (Sharkoon Skiller SGK55W) Generates Volume-Up Events on Linux When More Than 6 Keys Are Pressed Simultaneously

## Summary

A wireless 2.4 GHz keyboard produces unintended media key events on Linux when operating in wireless mode via its USB dongle.

The issue affects:

* Sharkoon Skiller SGK55W

### Core behavior

* Only occurs in **wireless mode (2.4 GHz dongle)**.
* Does **not occur in wired USB mode**.
* Appears when **7 or more keys are pressed simultaneously**.
* Does **not occur at 6 or fewer keys**.
* Disappears when **NKRO is disabled (6KRO mode)**.
* Reproduced across multiple Linux distributions and hardware.
* Not observed on Windows 11 (so far).
* Reproduced on two identical keyboard units.

---

## Operating Systems Tested

### Fedora systems

* Fedora Workstation 44
* Tested on two separate laptops
* Desktop environments:

  * GNOME
  * Sway

### Ubuntu system

* Ubuntu 26.04 Live USB
* Separate physical laptop

### Windows system

* Windows 11
* Same wireless dongle used

Result:

* Issue present on all Linux systems tested.
* Not observed on Windows 11 (no volume key events detected during testing).

---

## Hardware Setup

* Keyboard: Sharkoon Skiller SGK55W
* Connection modes:

  * Wired USB (stable)
  * 2.4 GHz wireless dongle (problematic)
* Keyboard includes:

  * Rotary encoder (volume knob)
  * VIA/QMK-compatible configuration interface
* Two identical units tested
* Same behavior on both units

---

## Initial Symptoms

While typing wirelessly, system volume would occasionally increase unexpectedly.

Reproducible inputs:

```text
asdfjkl;
```

```text
qweruiop
```

Also reproducible via:

* Holding `asdf`
* Pressing `jkl;` combinations

---

## Troubleshooting Steps Performed

* Tested across:

  * Fedora 44 (GNOME + Sway)
  * Ubuntu 26.04 Live USB
* Tested on multiple physical laptops
* Tested two identical keyboard units
* Verified both wired and wireless modes
* Moved dongle physically next to keyboard (no change)
* Verified no accidental encoder activation
* Reassigned encoder behavior in VIA
* Disabled all layers in configuration
* Set unused keys to `KC_NO`
* Observed raw input via:

```bash
sudo libinput debug-events
```

* Tested rollover behavior (6-key vs 7-key threshold)
* Toggled NKRO using:

```text
MAGIC_TOGGLE_NKRO
```

---

## libinput Evidence

When the issue occurs, Linux receives actual key events:

```text
KEY_VOLUMEUP (115)
KEY_UNKNOWN (240)
KEY_YEN (124)
KEY_HENKAN (92)
```

Observations:

* Events always appear together
* Same timestamp
* Same release timing
* Fully deterministic bundle

This confirms the issue is present at the kernel input layer (not GNOME/Sway).

---

## Key Reproduction Pattern

### 6 simultaneous keys (stable)

Example:

```text
asdfjk
```

Result:

* No volume changes
* No media key events

---

### 7 simultaneous keys (failure trigger)

Example:

```text
asdfjkl
```

Result:

```text
KEY_VOLUMEUP
KEY_UNKNOWN
KEY_YEN
KEY_HENKAN
```

This behavior is fully reproducible and consistent.

---

## NKRO Investigation

NKRO was toggled via VIA:

```text
MAGIC_TOGGLE_NKRO
```

### NKRO enabled (wireless)

* 7+ keys triggers rogue media events
* Volume changes occur

### NKRO disabled (6KRO)

* No volume changes
* No rogue key events
* Wireless mode becomes stable

---

## Key Findings

1. Issue only occurs in wireless mode.
2. Wired mode is fully stable.
3. Trigger is exactly at 7 simultaneous keys.
4. 6 or fewer keys do not trigger issue.
5. Occurs on Fedora Workstation 44.
6. Occurs on Ubuntu 26.04 Live USB.
7. Occurs on two separate laptops.
8. Occurs on two identical SGK55W keyboards.
9. Does not appear on Windows 11.
10. Same deterministic rogue key bundle always appears:

```text
KEY_VOLUMEUP
KEY_UNKNOWN
KEY_YEN
KEY_HENKAN
```

11. Disabling NKRO resolves the issue completely.

---

## Technical Analysis

Most likely failure point is the wireless NKRO report path.

Potential architecture:

```text
Wired mode:
Keyboard MCU
    → USB HID report A
    → Linux

Wireless mode:
Keyboard MCU
    → RF protocol
    → USB dongle firmware
    → USB HID report B
    → Linux
```

Failure appears when transitioning from 6-key rollover to NKRO mode.

Likely causes:

* Wireless NKRO firmware bug
* Dongle HID report decoding bug
* HID descriptor mismatch in wireless mode
* Linux kernel HID quirk missing for this device (less likely, but possible given recency)

The deterministic nature of the rogue keys strongly suggests a **bit-level misinterpretation of a HID report**, not RF noise or physical switch issues.

---

## Current Workaround

Disable NKRO and use 6KRO mode:

```text
MAGIC_TOGGLE_NKRO
```

Result:

* Stable wireless operation
* No volume key events
* No unintended media input

---

## Conclusion

The issue is a reproducible wireless NKRO failure affecting the Sharkoon Skiller SGK55W under Linux.

### Confidence ranking:

1. Wireless NKRO firmware/dongle bug — very high confidence
2. HID report descriptor mismatch (wireless path) — possible
3. Missing Linux HID quirk for new device — possible
4. Hardware defect — unlikely (two units affected identically)
5. Desktop environment issue — ruled out
6. Keymap configuration issue — ruled out

---

## Key Diagnostic Insight

The most important discovery:

> The system behaves normally up to exactly 6 simultaneous keys, and fails deterministically at 7 keys only in wireless mode.

This isolates the issue to the wireless NKRO transition boundary in the HID report pipeline.
