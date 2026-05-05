# TI Thermostat Firmware

Embedded C on a TI CC3220S LaunchPad. Reads temperature over I2C (auto-detects TMP116/117/006), buttons for setpoint control, LED for heater state, UART reporting at 115200 baud.

This one I'm actually proud of. The I2C sensor discovery loop - iterate addresses, probe, report which responded - is how I'd still do it today. The heater state machine keeps transitions and actions cleanly separated, which is a mistake I see people make constantly in embedded work.

What aged badly: the main loop is manual polling with hand-rolled elapsed-time counters. Fine for a school board, but an RTOS scheduler does this for free. Button debouncing by disabling interrupts is a hack that blocks everything else during the debounce window. And there are globals everywhere - `timer0`, `uart`, `i2c`, `setpoint`, `temperature` all floating around at file scope.

The integer truncation on the 0.0078125 temperature multiply bugs me now. Loses precision below about 5C.

**Keep.** Shows I2C, UART, GPIO, timer callbacks, and a proper state machine wired together on bare metal. It's the project that got me interested in hardware work beyond the classroom.
