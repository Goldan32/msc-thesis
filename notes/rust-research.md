# Using Rust with microcontrollers

Building general knowledge about how Rust is utilized in a microcontroller based system.

## General

- https://github.com/rust-embedded/awesome-embedded-rust#driver-crates Collection of rust embedded driver repos and resources.
- https://docs.rs/cortex-m-semihosting/latest/cortex_m_semihosting/ Remote debugging a Cortex M core.

## STM32H750

### Findings

https://crates.io/crates/stm32h7xx-hal

- A rust package that uses the HAL to access peripherals
- **Only the M7 core is supported on dual-core boards**
- Written fully in rust
- https://github.com/stm32-rs is proof of strong rust support for STM32-s
- **Ethernet peripheral is also supported**

Because a HAL was created, working on this mcu with rust would not be different than using C.

### TODOs

Some testing could be done to determine if using STM CubeIDE is necessary or possible. If not possible, then what is the way of configuring the pins.

See what needs to be done to support dual core applications. 

- Compiling for an M4 core is possible, peripherals can work the same.
- Concurrency checking peripherals (MPU) may need additional support.

## TI LP-AM243

### Findings

- No official support from manufacturer.
- As it is still a Cortex controller, only memory map and register definition is needed to compile.
- Peripheral drivers are not available, generalized HAL drivers that could be used here are also not available.
- https://pramode.net/2016/12/17/rust-on-tiva-launchpad/ Blog post describing how to create support for an unsupported board
- https://docs.rust-embedded.org/faq.html Does rust support my device
- https://github.com/rust-embedded/cortex-r Cortex-R rust repo

### TODOs

- Create HAL for this specific board, this means writing all necessary drivers from basically scratch
- Support multi-core applications, similarly hard as this task for the STM32

## Multi-core applications

- http://www.diva-portal.se/smash/get/diva2:1391552/FULLTEXT02.pdf Multi-core real time rust thesis
  - This should be read and understood in its entirity
  - Contains "Future work" section that could be used for ideas

## Rust and C in the same system

- Possible, there are many "wrapper" rust projects.
  - https://github.com/lobaro/FreeRTOS-rust compiles freertos from C and links it to a rust wrapper
  - This is broader than running C on one core and Rust on the other, so that should also be possible.
- Building a C-Rust hibrid example project and testing it can be done in a short time.
