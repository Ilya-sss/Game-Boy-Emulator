# Game Boy Emulator (CGBE)

A Game Boy emulator written in C using SDL2 for graphics and user interface.

## Overview

This project implements a Game Boy emulator capable of running original Game Boy ROM files. It features a modular architecture with separate components for CPU emulation, graphics rendering (PPU), memory management, input handling, and more.

## Features

- **CPU Emulation**: Full Game Boy CPU instruction set implementation
- **Graphics Rendering**: Picture Processing Unit (PPU) with pixel pipeline and state machine
- **Memory Management**: Memory bus, RAM, stack, and cartridge support
- **Input Handling**: Gamepad controller support
- **Display**: LCD rendering with SDL2
- **Interrupts**: Full interrupt system implementation
- **DMA**: Direct Memory Access controller
- **Timers**: Game Boy timer system
- **Debug Support**: Debugging utilities and tools
- **User Interface**: SDL2-based UI for interaction

## Requirements

### Dependencies

- **CMake** (version 3.10 or higher)
- **SDL2** (Simple DirectMedia Layer 2)
- **SDL2_ttf** (SDL2 TrueType font extension)
- **C Compiler** (GCC or Clang)

### Installing Dependencies

#### Ubuntu/Debian
```bash
sudo apt-get install cmake libsdl2-dev libsdl2-ttf-dev build-essential
```

#### Fedora/RHEL
```bash
sudo dnf install cmake SDL2-devel SDL2_ttf-devel gcc
```

#### macOS (using Homebrew)
```bash
brew install cmake sdl2 sdl2_ttf
```

## Building

1. Clone or navigate to the project directory:
```bash
cd /home/pc/Programming/C/part16
```

2. Create a build directory and configure:
```bash
mkdir -p build
cd build
cmake ..
```

3. Build the project:
```bash
make
```

The executable will be located at `build/cgbe/cgbe`.

## Usage

Run the emulator with a Game Boy ROM file:

```bash
./build/cgbe/cgbe <path_to_rom.gb>
```

Example:
```bash
./build/cgbe/cgbe ../roms/super_mario_land.gb
```

ROM files should be placed in the `roms/` directory or you can specify the full path to a ROM file.

## Project Structure

```
CBGE/
├── CMakeLists.txt          # Main CMake configuration
├── cgbe/                   # Main executable source
│   ├── CMakeLists.txt
│   └── main.c
├── lib/                    # Core emulator library
│   ├── CMakeLists.txt
│   ├── bus.c              # Memory bus implementation
│   ├── cart.c             # Cartridge handling
│   ├── cpu.c              # CPU main logic
│   ├── cpu_fetch.c        # CPU instruction fetching
│   ├── cpu_proc.c         # CPU processing
│   ├── cpu_util.c         # CPU utilities
│   ├── dbg.c              # Debug utilities
│   ├── dma.c              # DMA controller
│   ├── emu.c              # Emulator core
│   ├── gamepad.c          # Input handling
│   ├── instructions.c     # CPU instructions
│   ├── interrupts.c       # Interrupt system
│   ├── io.c               # I/O operations
│   ├── lcd.c              # LCD controller
│   ├── ppu.c              # PPU main
│   ├── ppu_pipeline.c     # Graphics pipeline
│   ├── ppu_sm.c           # PPU state machine
│   ├── ram.c              # RAM management
│   ├── stack.c            # Stack operations
│   ├── timer.c            # Timer system
│   └── ui.c               # User interface
├── include/               # Header files
├── roms/                  # Game Boy ROM files
├── tests/                 # Test suite
└── cmake/                 # CMake modules and scripts
```

## Components

### CPU
- Instruction fetch, decode, and execution
- Register management
- Flag handling

### PPU (Picture Processing Unit)
- Pixel pipeline for rendering
- State machine for different rendering modes
- Scanline and frame timing

### Memory
- Memory bus for address space management
- RAM handling
- Cartridge memory mapping

### Input/Output
- Gamepad controller input
- I/O port handling
- LCD display output

### System
- Interrupt controller
- DMA transfers
- Timer system
- Debug tools

## Testing

The project includes a test suite located in the `tests/` directory. To build and run tests:

```bash
cd build
make
# Run tests if available
```

## License

Check individual source files for license information.

## Contributing

This appears to be a learning/educational project. Feel free to extend functionality, fix bugs, or improve the codebase.

## Notes

- This emulator is a work in progress and may not support all Game Boy features or games
- ROM files are not included in the repository - you must provide your own legally obtained ROM files
- The emulator requires SDL2 for rendering and may have platform-specific considerations

## Troubleshooting

### Build Issues

- **SDL2 not found**: Ensure SDL2 development libraries are installed
- **CMake errors**: Verify CMake version is 3.10 or higher
- **Link errors**: Check that all SDL2 libraries are properly installed

### Runtime Issues

- Ensure ROM files are valid Game Boy ROMs (.gb format)
- Check that ROM file paths are correct
- Verify SDL2 rendering context can be created (check display/driver compatibility)

