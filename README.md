# renesas-bootmode
serial interface library for renesas microcontrollers in boot mode

## hardware
This library is tested using a FTDI FT232RL USB to serial adapter

(make sure you use one that can match Vcc of the microcontroller - 5V or 3.3V)

## SH-2A
```
+---+PC+---+          +---+FTDI+---+          +---+MCU+---+
|          |          |            |          |           |
|      USB +<-------->+ USB     RX +<-------->+ TX        |
|          |          |         TX +<-------->+ RX        |
|          |          |            |          |           |
|          |          |        GND +<-------->+ GND       |
|          |          |        VCC +<----*--->+ FLMD0     |
|          |          |            |     '--->+ RESET     |
|          |          |            |          |           |
+----------+          +------------+          +-----------+
```
### notes
* assumes MCU already has pull-up resistors on RX/TX lines
* assumes MCU already has pull-up resistor on RESET line
* momentarily set reset low then hold high to get into boot mode

## V850E2
```
+---+PC+---+          +---+FTDI+---+          +---+MCU+---+
|          |          |            |          |           |
|      USB +<-------->+ USB     RX +<------*->+ TX/RX     |
|          |          |         TX +<---o  |  |           |
|          |          |            |  ,-|>-'  |           |
|          |          |            |  |       |           |
|          |          |        GND +<-*------>+ GND       |
|          |          |        VCC +<-------->+ FLMD0     |
|          |          |        RTS +<---|>o-->+ RESET     |
|          |          |            |          |           |
+----------+          +------------+          +-----------+
```

### notes
* assumes MCU already has pull-up resistor on TX/RX line
* assumes MCU already has pull-up resistor on RESET line
* connect FTDI RTS line to inverter to MCU RESET line
* connect tri-state buffer
  * enable line wired to inverted FTDI TX
  * input line wired to GND
  * output line wired to TX/RX

## references
[Renesas Flash Programmer
Sample Circuit for Programming
by Using a PC’s Serial Port](https://www.renesas.com/us/en/doc/products/tool/doc/001/r20ut0857ej0300_rfpsplcrct.pdf)