# 555 Astable Timing Calculations

## Default Component Values

| Component | Value |
|-----------|-------|
| R1 | 1 kΩ (1,000 Ω) |
| R2 | 470 kΩ (470,000 Ω) |
| C1 | 10 µF (0.00001 F) |

## Frequency

```
f = 1.44 / ((R1 + 2×R2) × C1)
f = 1.44 / ((1,000 + 940,000) × 0.00001)
f = 1.44 / 9.41
f = 0.153 Hz
Period = 6.53 seconds
```

## High Time (LED ON)

```
t_high = 0.693 × (R1 + R2) × C1
t_high = 0.693 × 471,000 × 0.00001
t_high = 3.26 seconds
```

## Low Time (LED OFF)

```
t_low = 0.693 × R2 × C1
t_low = 0.693 × 470,000 × 0.00001
t_low = 3.26 seconds
```

## Duty Cycle

```
duty = (R1 + R2) / (R1 + 2×R2) × 100
duty = 471,000 / 941,000 × 100
duty = 50.05%
```

## Component Swap Reference

| C1 Value | Approx Frequency | Use Case |
|----------|-----------------|----------|
| 100 µF | 0.015 Hz | Very slow blink (67s) |
| 10 µF | 0.15 Hz | Default — slow blink |
| 1 µF | 1.5 Hz | Visible 1Hz blink |
| 0.1 µF | 15 Hz | Fast flash |
| 0.01 µF | 153 Hz | Audible tone (buzzer) |
| 0.001 µF | 1,530 Hz | Audio tone (~1.5kHz) |

Use [PickettCalc 555 Timer](https://pickettech.com/PickettCalc-555Timer.html) to calculate any custom values.
