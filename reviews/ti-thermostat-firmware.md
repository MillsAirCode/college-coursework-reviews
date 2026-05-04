# TI-Microcontroller-Thermostat-Firmware

https://github.com/MillsAirCode/TI-Microcontroller-Thermostat-Firmware

## what it was

Embedded C project for a smart thermostat running on a TI CC3220S LaunchPad. Part of my microcontroller coursework at SNHU. Reads temperature from a TMP116/117/006 sensor over I2C, exposes setpoint up/down buttons on GPIO, and drives an LED as a heater indicator. Reports status over UART at 115200 baud.

## what holds up

The I2C sensor auto-detection loop is clean -- iterate three known addresses, probe each, print which one responded. That's exactly how I'd write a sensor discovery routine today. The heater state machine (TickFct_Heater) is a simple two-state on/off with proper separation of transitions and actions. No action/transition mixing inside the same switch block, which is a common beginner mistake I avoided here.

## what I'd refactor

The main loop is a giant polling loop with manual elapsed-time counters incremented by fixed timer ticks. It works but it's the kind of thing a real RTOS task scheduler handles automatically. The button debouncing -- disable interrupts, wait, re-enable -- is a hack that blocks other interrupts during the debounce window. I'd use a software timer or edge-counting approach instead. Global variables everywhere (timer0, uart, i2c, setpoint, temperature) with no encapsulation. The `DISPLAY` macro that wraps UART2_write is fine for a class project but I'd at least use a proper logging function with format safety. The temperature reading has integer truncation on the 0.0078125 multiply that could lose precision on cold readings.

## portfolio take

Worth keeping as a link. Shows I2C, UART, GPIO interrupts, timer callbacks, and a basic state machine all wired together on bare metal. Not production quality, but it demonstrates the fundamentals of embedded systems work.
