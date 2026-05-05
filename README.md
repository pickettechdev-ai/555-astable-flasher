# 555-astable-flasher

A classic LED blinker using a 555 timer IC in **astable mode** — no microcontroller needed. This is one of the most fundamental electronics circuits and a great introduction to RC timing, duty cycle, and how the 555 timer works internally.

Part of the [PickettBuild](https://pickettech.com/PickettBuild.html) project series by [PICKETTECH](https://pickettech.com).

---

## What It Does

The 555 timer continuously oscillates, switching its output (Pin 3) ON and OFF at a frequency set by two resistors and a capacitor. A connected LED blinks at approximately **1Hz** with the default component values.

---

## Circuit

### Components

| Component | Value | Purpose |
|-----------|-------|---------|
| IC1 | NE555 / LM555 | Timer IC |
| R1 | 1 kΩ | Charge path upper resistor |
| R2 | 470 kΩ | Charge/discharge resistor |
| C1 | 10 µF | Timing capacitor |
| C2 | 0.01 µF (10nF) | Bypass capacitor on Pin 5 |
| R3 | 1 kΩ | LED current limiting resistor |
| LED1 | Any 5mm LED | Output indicator |
| V+ | 9V | Battery or supply |

### Pin Connections

```
Pin 1  (GND)     → GND
Pin 2  (TRIGGER) → Junction of R2, C1 (same as Pin 6)
Pin 3  (OUTPUT)  → LED anode via R3 (1kΩ) → GND
Pin 4  (RESET)   → VCC (keep HIGH to enable)
Pin 5  (CTRL V)  → GND via C2 (10nF bypass cap)
Pin 6  (THRESH)  → Junction of R2, C1 (same as Pin 2)
Pin 7  (DISCH)   → Junction of R1 and R2
Pin 8  (VCC)     → +9V
```

### Schematic (ASCII)

```
+9V ──┬─────────────────────── Pin 8 (VCC)
      │
      R1 (1kΩ)
      │
      ├── Pin 7 (DISCH)
      │
      R2 (470kΩ)
      │
      ├── Pin 6 (THRESH)
      ├── Pin 2 (TRIG)
      │
      C1 (10µF)
      │
GND ──┴────────────────────── Pin 1 (GND)

Pin 4 (RESET) ──────────────── +9V
Pin 5 (CTRL)  ──── C2 (10nF) ─ GND

Pin 3 (OUT) ─── R3 (1kΩ) ─── LED (+) ─── GND
```

---

## Frequency Calculation

In astable mode:

```
f  = 1.44 / ((R1 + 2×R2) × C1)
f  = 1.44 / ((1kΩ + 2×470kΩ) × 10µF)
f  ≈ 1.44 / (941,000 × 0.00001)
f  ≈ 0.15 Hz  (one flash every ~6.5 seconds)
```

> **To increase the flash speed**, reduce R2 or C1.  
> **To decrease the flash speed**, increase R2 or C1.

### Duty Cycle

```
t_high = 0.693 × (R1 + R2) × C1
t_low  = 0.693 × R2 × C1
duty   = (R1 + R2) / (R1 + 2×R2) × 100%
       ≈ 99.8% with these values (LED mostly ON)
```

To get a 50% duty cycle, replace R1 with a small value (100Ω) or add a diode across R2 to separate charge and discharge paths.

---

## Build Steps

1. Place the 555 IC across the centre divide of a breadboard
2. **Pin 8 → VCC**, **Pin 1 → GND**, **Pin 4 → VCC**
3. Wire **R1 (1kΩ)** from VCC to Pin 7
4. Wire **R2 (470kΩ)** from Pin 7 to the junction of Pin 6 and Pin 2
5. Wire **C1 (10µF)** from that junction to GND (observe polarity — positive leg to the junction)
6. Wire **C2 (10nF)** from Pin 5 to GND (decoupling cap)
7. Wire **R3 (1kΩ)** from Pin 3 to the LED anode; LED cathode to GND
8. Connect 9V supply — LED will begin blinking immediately

---

## Modifications & Extensions

| Modification | How |
|-------------|-----|
| Adjustable speed | Replace R2 with a 500kΩ potentiometer in series with 10kΩ fixed resistor |
| Faster blink (~5Hz) | Replace C1 with 2.2µF |
| Audio tone (~1kHz) | Replace C1 with 0.001µF, connect a small speaker instead of LED |
| 50% duty cycle | Add a 1N4148 diode in parallel with R2 (anode toward Pin 7) |
| Monostable trigger | Add a second 555 in monostable mode, triggered by a push button |
| Relay driver | Replace LED+R3 with a flyback-protected relay coil on Pin 3 |

---

## What You'll Learn

- How the 555 timer works internally (comparators, SR flip-flop, discharge transistor)
- RC time constant and its effect on oscillation frequency
- Duty cycle calculation and how to adjust it
- Breadboard wiring and component identification
- Reading a datasheet

---

## Troubleshooting

| Problem | Likely Cause | Fix |
|---------|-------------|-----|
| LED doesn't light at all | Pin 4 not tied to VCC | Connect Pin 4 to +9V |
| LED stays ON continuously | C1 wrong polarity or missing | Check electrolytic cap orientation |
| Very slow blink or no blink | C1 value too large | Check capacitor value (10µF not 100µF) |
| LED dim | R3 too high | Reduce R3 to 470Ω |
| Erratic behaviour | No bypass on Pin 5 | Add 10nF from Pin 5 to GND |

---

## Resources

- [PICKETTECH — PickettBuild Project Generator](https://pickettech.com/PickettBuild.html)
- [PICKETTECH — PickettCalc 555 Timer Calculator](https://pickettech.com/PickettCalc-555Timer.html)
- NE555 Datasheet — Texas Instruments

---

## Licence

This project is released under the [MIT Licence](LICENSE). Free to use, modify, and share.
