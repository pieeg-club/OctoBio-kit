# OctoBio-kit  
16-channel wireless EEG Octopus 16 (Powered by [XIAO-ESP32S3](https://www.seeedstudio.com/XIAO-ESP32S3-p-5627.html)) + Arduino starter kit: control real electronics with your brain, programmed with blocks in the browser.  

<img src="https://github.com/pieeg-club/OctoBio-kit/blob/main/Images/OctoBio%20kit.png" alt="general view" title="general view">  

# How to start  

<img src="https://github.com/pieeg-club/OctoBio-kit/blob/main/Images/octobio-how-to-start.gif" alt="general view" title="general view">  

Try OctoBio Studio right now, just in the [Browser](https://octobridge.pieeg.com/studio.html)  

# OctoBio Kit

**Brain rhythms in. Real-world actions out.**

OctoBio is a hands-on learning kit that links a wireless 16-channel EEG board to an Arduino starter kit. You can read your own brain signals, build simple block programs, and make lights, motors, sounds and screens respond. Everything runs in one browser tab.

🧪 **Open the lab:** [octobridge.pieeg.com](https://octobridge.pieeg.com/)
📖 **Docs:** [octoBridge docs](https://pieeg.com/docs/software/octobridge) · [Octopus 16 docs](https://pieeg.com/docs/hardware/devices/Octopus_16)
🛒 **Buy:** on [Elecrow](https://www.elecrow.com/) (SKU `PIA24028P`)

> ⚠️ **Not a medical device.** OctoBio is a tool for learning and experimenting. Focus and relax values are uncalibrated classroom indicators. Never use them for diagnosis or as a measure of mood or ability.

---

## Table of contents

- [What it is](#what-it-is)
- [What's in the box](#whats-in-the-box)
- [Quick start](#quick-start)
- [Lessons](#lessons)
- [What you can read and move](#what-you-can-read-and-move)
- [Block levels](#block-levels)
- [Flashing firmware](#flashing-firmware)
- [Technical details](#technical-details)
- [Troubleshooting](#troubleshooting)
- [Safety](#safety)
- [Support](#support)

---

## What it is

| | Brain side | Room side |
|---|---|---|
| **Device** | Octopus 16 EEG board | Elecrow All-in-One Starter Kit for Arduino (SEA0004T) |
| **Link** | Web Bluetooth | Web Serial (USB), 115200 baud |
| **Role** | Reads EEG and turns it into band power in the browser | Senses the room and acts on it |

The web app reads both devices at once and connects them with your blocks. You can also use either device on its own.

```
 Octopus 16 ──BLE──►┐
                    │   octobridge.pieeg.com   ┌──► LEDs, servo, buzzer,
                    ├──►  (Chrome / Edge tab)  ┤    relay, 16×2 LCD
 Starter kit ─USB──►┘   blocks: if / then      └──◄ light, distance, PIR,
                                                    temp, soil, knob ...
```

**What students learn**

- **Biology:** brain rhythms (δ θ α β γ), why alpha rises when the eyes close, and the artifacts that blinks and jaw clenches leave in the signal.
- **Electronics:** sensors and actuators, analog vs digital, I²C, serial communication, units and ranges.
- **Programming:** if / else, loops, thresholds, mapping one range onto another, and combining two signals into one decision.

---

## What's in the box

**Included**

- 1 × Octopus 16 EEG board (with Seeed Studio XIAO ESP32-S3 and BLE antenna)
- 1 × Elecrow All-in-One Starter Kit for Arduino (SEA0004T), in its case
- Access to the OctoBio web app and firmware

**Not included**

- A small 5 V power bank for the Octopus 16 (worn on the head)
- A computer with Bluetooth running **desktop Chrome or Edge**
- USB **data** cables, if you don't already have them (charge-only cables can't flash or stream)

---

## Quick start

1. **Open the lab.** Go to [octobridge.pieeg.com](https://octobridge.pieeg.com/) in desktop Chrome or Edge. You don't need an account or an install. Safari, Firefox and phones won't work, because they lack Web Bluetooth and Web Serial.
2. **Flash once.** Open **Flash**, plug each board in with a USB data cable, and install its firmware from the browser. You don't need the Arduino IDE. See [Flashing firmware](#flashing-firmware).
3. **Connect.** Open **Connect**.
   - Power the Octopus 16 from the **power bank**, then pick `Octopus-16-XXXX` in the Bluetooth picker.
   - Plug in the starter kit and pick its serial port. The board restarts, so wait until the status says **live**.
4. **Put it on.** Strap the Octopus 16 over the **back of the head** (visual cortex) and press it straight down so every pin touches the scalp. **Use battery power only.**
5. **Check the signal.** On **Board**, look for a green **EEG ok** (RMS between 2 and 200 µV), then try these two tests:
   - Close your eyes for 10 seconds. Alpha should rise, then drop when you open them.
   - Blink and clench your jaw. RMS and gamma should jump, then settle. That's muscle, not a thought.
6. **Build.** Open **Blocks**, stack `forever` → `if` → an action, and press **Run**. The program runs live, with no compiling.

```
forever
  if  alpha is high
      light D10 on
  else
      light D10 off
```
*Eyes closed → alpha rises → the LED turns on.*

> 💡 No headset yet? Start with the **Follow the knob** lesson. It uses only the starter kit.

### Lab pages

| Page | What it does |
|---|---|
| **Home** | What you can read, what you can move, ready mixes |
| **Flash** | Put firmware on the boards (first time only) |
| **Connect** | Pair the Octopus 16 and/or the starter kit |
| **Board** | Live numbers, lights, motor and screen |
| **Blocks** | Stack a program and run it |
| **Learn** | Lessons on what a reading is allowed to mean |
| **Write** | The same program, written like a page |
| **Repeat** | Six ready machines to run and remix |

---

## Lessons

Each lesson is a single rule (**one condition, one action**), so cause and effect are obvious straight away.

| Lesson | Signal → Action | Needs headset | Concepts |
|---|---|:---:|---|
| Eyes closed, light on | alpha > 35% → LED D10 | ✅ | Alpha rhythm, if / else, threshold |
| Focus meter | focus index → servo angle | ✅ | Mapping a range, beta band |
| Quiet room | alpha high **and** no motion → LCD | ✅ | Combining two signals, PIR |
| Follow the knob | knob (0–1023) → servo (0–180°) | ❌ | Analog input, mapping |
| Plant care | soil < 300 → buzzer | ❌ | Raw ADC counts, threshold |
| Blink is not a thought | RMS > 45 µV **or** gamma > 22% → LCD "artifact!" | ✅ | Artifacts, signal quality, OR logic |

---

## What you can read and move

**Read: Octopus 16**

- Relative band power: delta, theta, alpha, beta, gamma
- Focus and relax (uncalibrated indexes)
- RMS (µV), the strongest band, and an "EEG ok" check

**Read: starter kit**

| Sensor | Part | Unit |
|---|---|---|
| Light | BH1750 | lux |
| Distance | Ultrasonic | cm (needs a facing surface; a missed echo is a negative number) |
| Temperature & humidity | DHT20 | °C, % |
| Motion | PIR | yes / no |
| Tilt | MPU6050 | 6-axis, no heading |
| Sound, soil moisture, knob | analog | raw 0–1023 (not calibrated) |
| Button, IR remote | digital | pressed / codes |

**Move: starter kit**

| Output | Commands |
|---|---|
| Light D10 | on, off, flash |
| Light D8 | on, off |
| Servo | 0–180° |
| Relay | on, off (**never connect it to mains**) |
| Buzzer | on, off |
| 16×2 LCD | two lines of text |

---

## Block levels

The same kit and the same lessons work at every level. Move up a level as the class does.

| Level | Name | Audience |
|:---:|---|---|
| 1 | Story | Primary school |
| 2 | Words | |
| 3 | Bands (δ θ α β γ) | |
| 4 | Measure (numbers and units) | |
| 5 | Raw (raw values) | University |

---

## Flashing firmware

Do this once, from [octobridge.pieeg.com/flash](https://octobridge.pieeg.com/flash), in Chrome or Edge with a USB data cable.

**Octopus 16 (XIAO ESP32-S3)**

1. Plug the XIAO into the computer.
2. Click **Install Octopus-16** and choose its port.
3. No port showing? Hold **BOOT**, tap **RESET**, release BOOT, and install again.
4. Unplug and replug when it finishes. It now appears over Bluetooth as `Octopus-16-XXXX`.

**Starter kit (Arduino Uno / ATmega328P)**

1. Close any other serial monitor (Arduino IDE, terminal).
2. Click **Flash octoBio Kit** and choose the port. Flashing takes about 20 seconds.
3. The screen should say **octoBio Kit Ready**.

Supported: official Uno (16U2) or CH340 clones. Not supported: Leonardo, Mega, ESP32 boards, or boards without a bootloader.

---

## Technical details

### Specifications

| | Octopus 16 | Starter kit |
|---|---|---|
| **MCU** | Seeed Studio XIAO ESP32-S3 | ATmega328P (Uno compatible) |
| **Channels / IO** | 16 EEG, dry spring-loaded pogo pins | 10 sensors, 6 outputs |
| **ADC** | 2 × TI ADS131M08, 24-bit, gain 4 | 10-bit (0–1023) |
| **Link** | Bluetooth LE, ~250 SPS | USB serial, 115200 baud |
| **Power** | 5 V power bank (battery only while worn) | USB |

> ℹ️ **Sample rate:** the firmware advertises 250 SPS. With the current 8.000 MHz ADC clock the true rate is about **244 SPS** (4 MHz / OSR 16384). That's fine for viewing and band power, but correct for it if you do precise timing work (ERP / P300).

### Octopus 16 BLE protocol

| Item | Value |
|---|---|
| Service | `4fafc201-1fb5-459e-8fcc-c5c9c331914b` |
| Data (NOTIFY) | `beb5483e-36e1-4688-b7f5-ea07361b26a8` |
| Cmd (WRITE) | `c0de0001-36e1-4688-b7f5-ea07361b26a8` (register bridge) |
| Name | `Octopus-16-XXXX` |

**Packet: 51 bytes, one sample per notification**

| Bytes | Meaning |
|---|---|
| `[0]` | `0xA0` start |
| `[1]` | sample counter (0–255) |
| `[2..25]` | ADC1, ch 0–7 (8 × 3-byte big-endian signed 24-bit) |
| `[26..49]` | ADC2, ch 8–15 |
| `[50]` | `0xC0` end |

```
µV = raw × (1.2 / 4.0 / 8388607) × 1e6
```

### Use the Octopus 16 in your own web app

```html
<script src="https://cdn.jsdelivr.net/gh/pieeg-club/PiEEG-server@main/pieeg.js"></script>
<button id="connect">Connect</button>
<script>
  const eeg = new PiEEG();
  eeg.onBandPowers(p => console.log('alpha', p.Alpha, 'focus', eeg.getFocusIndex()));
  document.getElementById('connect').onclick = () =>
    eeg.connectBLE({ device: 'octopus-16' });   // must be called from a click
</script>
```

See the [JavaScript SDK docs](https://pieeg.com/docs/software/api/javascript-sdk). The Octopus 16 also works on [cloud.pieeg.com](https://cloud.pieeg.com).

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Lab won't connect | Use **desktop** Chrome or Edge over HTTPS. Safari, Firefox and phones are not supported. |
| No serial port when flashing | Use a **data** cable, not a charge-only one. Close the Arduino IDE and other serial monitors. |
| XIAO not detected | Hold BOOT, tap RESET, release BOOT, then retry. |
| Octopus silent after flash | Unplug and replug the USB once. |
| Octopus visible on Bluetooth but no EEG data / LED double-blinks | The XIAO is seated the wrong way round (rotated 180°). Reseat it so the `5V / GND / 3V3` labels line up. |
| Connects then drops | Retry the connection, then sit still for the first run. |
| "EEG ok" stays red | Press the board straight down so every pin touches the scalp, and keep still. Clean the pins with isopropyl alcohol. |
| Kit numbers don't move | Wait for **live** after the port opens (the board restarts). |
| Distance shows a negative number | The echo was missed. Point the sensor at a facing surface. |

**Pogo pin care:** clean the pins with IPA (>90%) and use compressed air for dust. Press straight down and never sideways. To free a stuck pin, put a drop of IPA in the barrel, gently work the plunger, and let it dry. **Never use oil or grease.**

---

## Safety

**Read this before anyone puts the kit on.**

- 🔋 **Wear the Octopus 16 on battery power only.** Never wear it while it's plugged into a computer or a wall charger. The board has no isolation from its power supply. USB is only for flashing, with the board off the head.
- ⚡ **Never connect the relay to mains voltage.**
- 🩺 The kit is **not a medical device** and is not certified by any regulator for use on the human body.
- ❤️ If someone has a pacemaker or other implanted device, ask a physician before use.
- 🧴 Stop if the skin becomes irritated.
- 📊 Focus and relax are uncalibrated learning indicators, not a diagnosis.

---

## Support

The PiEEG team supports the OctoBio software, firmware and the Octopus 16:

- 💬 [Discord](https://discord.gg/5Ps24p47)
- 🐙 [GitHub, PiEEG Club](https://github.com/pieeg-club)
- ✉️ pieeg@pieeg.com

---

## License

<!-- Add your license here, e.g. MIT -->

© PiEEG · OctoBio Kit
