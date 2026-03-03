<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

This project implements an SPI-controlled PWM peripheral.  
An SPI controller communicates with the design using three signals: SCLK, COPI, and nCS.  
SPI transactions are used to write data to internal registers that control the behavior of the outputs.

Each SPI transaction contains:
- 1 bit for read/write
- 7 bits for the register address
- 8 bits of data

The SPI peripheral decodes these transactions and stores the data in registers.  
These registers control whether each output is enabled and whether the output generates a constant signal or a PWM signal.

The PWM module generates a PWM signal with a frequency of approximately 3 kHz.  
The duty cycle of the PWM signal is controlled by the value written to the `pwm_duty_cycle` register.

The outputs are organized into a 16-bit structure:
`{uio_out[7:0], uo_out[7:0]}`

Each output can be independently configured to output:
- 0 (disabled)
- 1 (constant high)
- a PWM signal.


## How to test

The project is tested using cocotb testbenches.

The SPI testbench verifies that:
- SPI transactions are decoded correctly
- register values are written properly
- invalid addresses are ignored

The PWM testbench verifies:
- PWM frequency is approximately 3 kHz
- PWM duty cycle matches the configured register value
- the interaction between the output enable and PWM enable registers behaves correctly.

## External hardware

No external hardware is required.  
The design is verified entirely through simulation using the provided testbenches.