# Genan Omer

## 30 June 2025

Finishing Tour of Rust and Rustlings exercises.

## 1 July 2025

Doing most of the labs using a STM32. Recalling what I learned.

## 2 July 2025

Reading more about TockOS and technical details about the NXP-LPC55 board. Starting to work on a issue related to a NXP board really soon.

## 3 July 2025

Installing Tock, libtock-c, and libtock-rs, and starting to experiment with them (building a small app, flashing an STM32F429ZI with Tock), as well as reading more about the TockOS architecture.

## 4 July 2025

Reading about how to write the TockOS kernel and how to boot the NXP LPC55 board. Next week, I will start working on the issue alongside Vlad.

## 7 July 2025

Started working on the issue today. I began by learning how to open the debug probe on the board. Then I started looking into the memory mapping of the board and began writing the layout.ld file.

After creating the layout.ld file, Vlad identified the architecture for the Cortex-M33 and added it to Tock. Before that, we began writing the other required components (the chip file and the board file), but we ran into a problem.

After building the program and attempting to flash it to the board using probe-rs, we encountered an error related to the build file. Specifically, the sections are not being created properly on the chip, and the flashing process is failing.

We tried several solutions, but haven’t made any progress yet. We’ll look into it further tomorrow.
