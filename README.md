# PineCone Rust Blinky
A simple example program using the [BL602 Rust HAL](https://github.com/sipeed/bl602-hal) and [PineCone](https://wiki.pine64.org/wiki/PineCone) BL602 evaluation board.

## Installation
If you don't have Rust and Cargo installed, install the stable toolchain using rustup from https://rustup.rs/ 

This project was tested with following setup:
```
rustup install nightly-2022-12-25
rustup component add llvm-tools-preview --toolchain nightly-2022-12-25
rustup target add riscv32imac-unknown-none-elf

cargo install cargo-binutils
```
One of the official [Bouffallo Lab](https://en.bouffalolab.com/) flash tool is used:

```
pip install bflb-mcu-tool
```

You can generate firmware:

```
cargo objcopy --release -- -O binary pinecone-blinky.bin
```

Flash it to PineCone board (Set the PineCone jumper (IO 8) to the L position and press the reset button):

```
bflb-mcu-tool --chipname bl602 --firmware pinecone-blinky.bin
```

Set the  to normal mode (Set the PineCone jumper (IO 8) to the H position) and restart the board. Connect to PineCones’s UART port at 2 Mbps like so:

```
tio -b 2000000 /dev/cu.usbserial-14160 
[22:21:24.559] tio v2.5
[22:21:24.560] Press ctrl-t q to quit
[22:21:24.565] Connected
LEDs off
LEDs on
```

You should also see blue led blinking:

![blinky](blinky.gif)