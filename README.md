# EmberRTOS v6.1
A monolithic micro‑OS for the ESP32‑S3.  
Binary‑only release. Made by a random bored 12‑year‑old lol.

EmberRTOS is a compact, single‑loop monolithic kernel designed for the ESP32‑S3.  
It operates without FreeRTOS, without ESP‑IDF, and without any external libraries.  
Every subsystem—filesystem, command parser, applications, and error handling—runs  
inside one continuous execution loop.

This project is distributed as a binary‑only release.

---

## Overview

EmberRTOS is technically a Real‑Time Operating System because:

1. It runs in a deterministic single‑loop execution model.  
2. Every command, file operation, and application executes in bounded, predictable time.  
3. The kernel never context‑switches or schedules tasks; instead, it processes events  
   in strict order, guaranteeing consistent timing behavior.  
4. The CLOCK and CALC applications demonstrate real‑time behavior with stable updates  
   and no jitter caused by background tasks.

Although EmberRTOS is extremely small, its behavior is consistent, predictable,  
and time‑accurate—meeting the core definition of a real‑time system.

---

## Architecture

EmberRTOS is a **monolithic kernel**, meaning:

- All functionality runs in a single memory space.  
- There is no separation between kernel and user code.  
- All commands, apps, and filesystem operations execute inside one loop.  
- There is no scheduler, no threads, and no interrupts used for OS logic.  
- The kernel directly manages flash and RAM without abstraction layers.

This design is simple, deterministic, and extremely fast on microcontrollers.

---

## The “Cursed Secret”: Tape‑RAM

EmberRTOS uses a custom memory model inspired by vintage tape‑based systems.  
Instead of a modern filesystem, it stores data in a linear sequence of blocks  
that behave like a virtual tape:

- Folders and files are stored as sequential entries.  
- Deleting a file rewrites the tape structure.  
- Reading a file walks the tape from the beginning.  
- The manifest acts as a directory index for faster lookup.  
- All content is stored as raw bytes without a filesystem driver.

This design is unusual, but it makes the OS extremely small and predictable.  
It also allows EmberRTOS to run without any external libraries or drivers.

---

## Command System

### Directory Commands
- **MKDIR FolderName**  
  Creates a new folder.

### File Commands
- **MKTXT<Folder><Filename><"Content">**  
  Creates a text file with full support for spaces and quoted content.

- **CAT<Folder>**  
  Lists all files inside a folder.

- **CAT<Folder><Filename>**  
  Reads the content of a text file.

- **EDIT<Folder><Filename>**  
  Opens a file for editing.

- **DELETE<Folder>**  
  Deletes a folder and all contents.

- **DELETE<Folder><Filename>**  
  Deletes a specific file.

### Applications
- **CLOCK**  
  Displays a live ASCII analog clock.  
  Use `EXIT` to close.

- **CALC<Op><Val1><Val2>**  
  Performs arithmetic operations.

- **CALC<TrigOp><Degrees>**  
  Performs trigonometric calculations.

### System Commands
- **HELP**  
  Shows the command index.

- **EXIT**  
  Leaves CLOCK or CALC.

- **SHUTDOWN**  
  Commits all blocks and halts the kernel.

---

## Flashing

### Using esptool.py
esptool.py write_flash 0x10000 EmberRTOS.bin
OR

### Using the Web Flasher
Flash at address **0x10000** using:  
https://espressif.github.io/esptool-js/

---

## License

See `LICENSE` for binary‑only usage terms.  
You may use EmberRTOS, but you may not claim ownership, modify it, or reverse engineer it.


HAVE FUN MY INVENTORS HEHEHAHAHAHA

<img width="228" height="148" alt="image" src="https://github.com/user-attachments/assets/f2f2adcb-a8a7-4e5e-9b5c-6c1e9ebe4ed0" />

