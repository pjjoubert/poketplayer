# Portable Music & Audiobook Player
**Project Brief | Quicksave v0.1**

## 1. Project vision

Build a compact, self-contained portable music and audiobook player inspired by the classic Apple iPod.

The goal is a practical, reliable device with:
- Local music and audiobook playback.
- Removable media storage.
- Physical playback controls.
- A touchscreen interface.
- A standard 3.5 mm headphone output.
- Excellent battery life, targeting approximately 20 hours.
- Custom software developed specifically for the device.

The project prioritises usability, portability, battery efficiency and maintainability.

## 2. Hardware decisions

| Component | Current decision |
|---|---|
| Main board | Raspberry Pi Zero 2 WH |
| Display | Adafruit PiTFT Plus 2.8", 320 × 240, capacitive touchscreen |
| Display orientation | Portrait |
| Audio | Dedicated I²S DAC with headphone amplifier |
| Headphone output | Standard 3.5 mm jack |
| Media storage | Removable microSD via USB reader |
| Operating system storage | Separate onboard microSD |
| Battery | Replaceable 21700 Li-ion cells |
| Charging | USB-C |
| Target runtime | Approximately 20 hours |

**Selected display:** [Adafruit PiTFT Plus 2.8" from PiShop](https://www.pishop.co.za/store/adafruit-pitft-plus-320x240-28-tft---capacitive-touchscreen40-pin?key=983)

**DAC candidate:** InnoMaker HiFi DAC Mini, using PCM5122 DAC and TPA6133 headphone amplifier. Physical compatibility with the display stack still needs verification.

## 3. Power subsystem

Power efficiency is a major design consideration.

Target:
- Approximately 20 hours of playback.
- Compact battery arrangement.
- Proper battery protection.
- Regulated 5 V supply with sufficient current headroom.
- Safe charging while the device is operating.
- Battery monitoring accessible to the player software.

### Shortlisted candidate

**Waveshare UPS HAT (D)**

[Manufacturer documentation](https://www.waveshare.com/wiki/UPS_HAT_(D))

[PiShop South Africa listing](https://www.pishop.co.za/store/5v-ups-hat-d-for-raspberry-pi-for-21700-batteries?keyword=21700&category_id=0)

Features:
- Two parallel 21700 batteries.
- Regulated 5 V output.
- Advertised maximum output of 2.5 A.
- USB-C charging.
- Power-path management.
- Battery protection.
- I²C battery monitoring.

**Status: Shortlisted, not purchased.**

Main concern: physical size (56 × 85 mm) and suitability for the compact enclosure. Rewiring or independent mounting may be considered if necessary.

Alternative custom power-management solutions remain under consideration. Engineering friends will also be consulted.

## 4. Enclosure and industrial design

Design direction: classic iPod proportions, without attempting an exact replica.

Agreed characteristics:
- Portrait orientation.
- Screen positioned in the upper portion of the front face.
- Separate physical buttons instead of a click wheel.
- Flush, discreet button styling.
- Rounded corners and a comfortable curved rear shell.
- Headphone and USB-C connections on the bottom edge.
- Accessible removable media.
- Replaceable battery arrangement.

The enclosure dimensions are not yet fixed. They must be determined from the actual component layout, with portability a priority. Avoid creating a bulky device simply to accommodate oversized electronics.

## 5. Software architecture

Build the player application from scratch for complete control over functionality and user experience.

Do not reinvent operating systems, audio codecs or hardware drivers. Use established Linux interfaces and libraries.

Proposed stack:

| Area | Technology |
|---|---|
| Language | C |
| UI | LVGL |
| Audio | ALSA |
| Metadata | TagLib |
| Persistence | SQLite |
| Hardware interfaces | Linux GPIO / SPI / I²C |
| Startup | systemd |
| Build system | CMake |
| OS | Raspberry Pi OS Lite, 64-bit |

Proposed software modules:

- `core` – application lifecycle and playback coordination.
- `audio` – playback, queue and audio output.
- `library` – media scanning and metadata.
- `storage` – removable media management.
- `ui` – touchscreen interface.
- `input` – physical buttons and touch input.
- `power` – battery monitoring and power management.

Wi-Fi and Bluetooth should be disabled during normal operation unless a future feature requires them.

## 6. Physical controls

Proposed controls:

- Previous track.
- Play/Pause.
- Next track.
- Volume down.
- Volume up.
- Power / screen lock.

Buttons should be flush-mounted and discreet, with sufficient tactile feedback to operate without looking at the device.

Long-press actions can provide secondary functions.

## 7. Outstanding decisions and investigations

1. Final battery and power-management solution.
2. Confirm DAC and display physical stacking compatibility.
3. Establish actual power consumption through measurement.
4. Confirm battery runtime under realistic playback conditions.
5. Determine final enclosure dimensions.
6. Design internal component arrangement and mounting.
7. Finalise physical button placement.
8. Develop the software architecture and initial playback prototype.

## 8. Development philosophy

- Prefer open-source components and software.
- Prioritise efficiency over unnecessary complexity.
- Measure rather than assume, particularly regarding power consumption.
- Keep hardware modular and replaceable where practical.
- Build incrementally and test individual subsystems before integration.
- Keep the device genuinely portable. No bricks disguised as music players!

---

**Current project status:** Concept and primary platform selected. Display and DAC candidates identified. Power subsystem under investigation. Mechanical design direction established. Software architecture proposed.

**Next milestone:** Finalise the power subsystem and internal hardware arrangement before committing to enclosure dimensions or purchasing all components.
