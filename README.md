# MyWhoosh Pad (`mywhoosh_keyboard`)

A wireless 18-button cycling controller (BLE HID keyboard) based on the **SuperMini nRF52840** and **ZMK** firmware, designed to control the **MyWhoosh** indoor cycling simulator (along with Windows/Android media controls) directly from your handlebars.

---

## Microcontroller (`SuperMini nRF52840`)

This project uses the **ProMicro / SuperMini nRF52840** board revision with USB Type-C and three additional through-hole pads (`101`, `102`, `103`) located right above the antenna:

<p align="center">
  <img src="board.jpg" alt="SuperMini nRF52840" width="320">
</p>

---

## Key Features
* **18 independent physical buttons** without a diode matrix (direct pin-to-`GND` wiring).
* **Bluetooth Low Energy (BLE 5.0):** fast automatic reconnection to PC and smartphones.
* **Battery level reporting** natively displayed in Windows 10/11 and Android Bluetooth settings.
* **Power saving:** enters `Deep Sleep` after 40 minutes of inactivity and wakes up instantly upon pressing any button.
* **Accidental reset protection:** clearing Bluetooth pairing (`BT_CLR`) requires holding down two physically separated buttons simultaneously.

---

## Keymap & Pinout (`SuperMini nRF52840`)
Each button connects one terminal to the specified GPIO pin and the other to a common **`GND`** rail. A `3.7V Li-Po` battery connects to the **`B+`** and **`B-`** pads.

| # | ZMK Keycode | Action in MyWhoosh / OS | Board Label | Board Position | ZMK Pin |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **1** | `K` | Virtual Gear Up | `006` | Left row, 1st below `B-` | `pro_micro 1` |
| **2** | `I` | Virtual Gear Down | `008` | Left row, 2nd below `B-` | `pro_micro 0` |
| **3** | `A` | Turn Left / Route Selection | `017` | Left row (below the two `GND` pins) | `pro_micro 2` |
| **4** | `D` | Turn Right / Route Selection | `020` | Left row | `pro_micro 3` |
| **5** | `U` | U-Turn (180°) | `022` | Left row | `pro_micro 4` |
| **6** | `1` | Camera View 1 | `024` | Left row | `pro_micro 5` |
| **7** | `2` | Camera View 2 | `100` | Left row | `pro_micro 6` |
| **8** | `3` | Camera View 3 | `011` | Left row | `pro_micro 7` |
| **9** | `4` | Camera View 4 | `104` | Left row | `pro_micro 8` |
| **10** | `5` | Camera View 5 | `106` | Bottom-left pin | `pro_micro 9` |
| **11** | `6` | Camera View 6 | `101` | Through-hole pad above antenna | `gpio1 1` |
| **12** | `7` | Camera View 7 | `102` | Through-hole pad above antenna | `gpio1 2` |
| **13** | `C_VOL_DN` | Volume Down | `111` | Right row | `pro_micro 14` |
| **14** | `C_VOL_UP` | Volume Up | `113` | Right row | `pro_micro 15` |
| **15** | `C_PREV` | Previous Track | `115` | Right row | `pro_micro 18` |
| **16** | `C_NEXT` | Next Track | `002` | Right row | `pro_micro 19` |
| **17** | `C_PP` | Play / Pause *(+ #18 = BT Clear)* | `029` | Right row | `pro_micro 20` |
| **18** | `LG(PSCRN)` | Screenshot to Pictures folder *(+ #17 = BT Clear)* | `031` | Right row (below `VCC`) | `pro_micro 21` |

---

## Power & Bluetooth Management
* **Clear Bluetooth Pairing (`BT_CLR`):** press and hold buttons **#17 (`029`)** and **#18 (`031`)** (Play/Pause + Screenshot) simultaneously. This erases the current bond and puts the controller into pairing mode.
* **Bootloader Mode (Flashing):** double-tap **`RST`** to **`GND`** — the board will mount as a removable USB drive named `NICENANO` where you can drag and drop the `.uf2` firmware file.

---

## Building Firmware (GitHub Actions)
1. Any commit to `config/` or `boards/shields/macropad/` automatically triggers a firmware build in the **Actions** tab.
2. Open the latest successful workflow run and download the **`firmware`** artifact.
3. Extract **`macropad-nice_nano_v2-zmk.uf2`** and copy it onto the `NICENANO` drive.
