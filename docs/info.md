## How it works

This design drives a seven-segment display through a repeating 4-7-8 breathing sequence. With a 1 Hz clock, it counts up from 1 to 4 for IN, 1 to 7 for HOLD, and 1 to 8 for OUT. The complete cycle takes 19 clock periods.

The decimal point identifies the phase: off during IN, continuously on during HOLD, and blinking with the clock during OUT.

Nineteen D flip-flops form a one-hot ring. A synchronous active-low reset sets the first IN state and clears the other states. Each rising clock edge advances the active state. OR gates select the digit, and a logic decoder generates the seven display segments.

Outputs 0 through 6 drive segments A through G respectively. Output 7 drives the decimal point. All display outputs are active high. The eight general-purpose inputs are unused. The circuit requires a 1 Hz clock for one-second counts and does not include a clock divider.

## How to test

In Wokwi, start the simulation and select the automatic clock using the small switch toward the clock generator. The generator should be set to 1 Hz. Hold RESET for about two seconds, then release it. Reset must overlap at least one rising clock edge.

Check that the display repeats 1-4 with the dot off, 1-7 with the dot on, and 1-8 with the dot blinking. The dot should blink starting at OUT 1.

For manual testing, select the Step button as the clock source. Hold RESET, press and release Step once, then release RESET. This establishes IN 1. Each subsequent Step advances one state: four steps reach HOLD 1, eleven reach OUT 1, and nineteen return to IN 1. In manual OUT mode, the dot is on while Step is held.

On hardware, provide a 1 Hz clock and assert RST_N low through a rising clock edge before observing the same sequence.

## External hardware

A common-cathode seven-segment display with a decimal point is used as the indicator. Physical display connections require suitable current limiting. The Wokwi project includes the display, a 1 Hz clock generator, a clock-selection switch, and Step and RESET buttons for simulation.
