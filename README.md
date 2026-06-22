# Joker

**Joke app showing a 270×270 bouncing window with Joker pashalko sound and GIF**

[![VirusTotal Scan](https://img.shields.io/badge/VirusTotal-Scan-blue)](https://www.virustotal.com/gui/file/b8eb0232544fc38c46072e71256e41df1949a95f23f1350081cfe1b2c5a4693d)

---

## About

Joker is a lightweight Windows desktop application that displays a small 270×270 pixel window featuring an animated Joker GIF. The window bounces around the screen like a DVD screensaver, while a looping sound plays in the background. It is designed to be a humorous prank or an easter‑egg style application that can be placed in the Windows autostart folder.

---

## Features

- 270×270 pixel borderless window
- Bouncing animation that moves the window across the screen
- Animated Joker GIF displayed inside the window
- Looping Joker sound effect (played asynchronously)
- Window stays always on top (`WS_EX_TOPMOST`)
- No taskbar icon (`WS_EX_TOOLWINDOW`)
- Can be placed in Windows autostart for automatic launch on login

---

## Requirements

- **Operating System:** Windows (tested on Windows 10/11)
- **Compiler:** MinGW‑w64 (or any GCC‑compatible toolchain with Windows resource compiler support)
- **Libraries:**
  - GDI+ (`gdiplus`)
  - Windows Multimedia API (`winmm`)
  - OLE32 (`ole32`)
  - Standard C++ libraries

---

## Compilation

The project uses a resource script to embed the GIF and sound files directly into the executable.

### 1. Prerequisites

- Install [MinGW‑w64](https://www.mingw-w64.org/) with `windres.exe` (resource compiler) and `g++`.
- Ensure the following files are present in the project directory:
  - `joker.cpp` – main source code
  - `resource.rc` – resource definition
  - `resource.h` – resource identifiers
  - `joker.gif` – the animated GIF
  - `jokersound.wav` – the sound file

### 2. Compile using windres and g++

The exact compilation commands (from `compile.txt`) are:

    windres resource.rc -O coff -o resource.res.o
    g++ -static -static-libgcc -static-libstdc++ joker.cpp resource.res.o -o joker.exe -lgdi32 -lgdiplus -lole32 -lwinmm

This produces a standalone `joker.exe` with all resources embedded.

---

## Usage

Simply run `joker.exe`. A 270×270 window will appear and start bouncing around the screen. The sound will loop continuously until the process is terminated.

### Auto‑start (xd)

To have Joker launch automatically when Windows starts:

1. Press `Win + R`, type `shell:startup` and press Enter.
2. Copy `joker.exe` into the Startup folder that appears.

Alternatively, you can add a registry entry or create a scheduled task.

---

## VirusTotal Scan

The compiled executable has been scanned with VirusTotal.  
You can view the scan results here:  
[link](https://www.virustotal.com/gui/file/b8eb0232544fc38c46072e71256e41df1949a95f23f1350081cfe1b2c5a4693d)

*Note: As with many small Windows executables that use uncommon APIs or packers, some antivirus engines may produce false positives. Always verify the source code before running.*

---

## How It Works

1. **Window Creation** – Creates a borderless, always‑on‑top window sized 270×270 pixels.
2. **GIF Loading** – Loads the animated GIF from embedded resources using GDI+.
3. **Animation** – Uses a timer to advance GIF frames and redraw the window.
4. **Bouncing** – Updates window position by adding velocity (`x`, `y`) and reverses direction when hitting screen edges.
5. **Sound** – Plays the embedded WAV file in a separate thread using `sndPlaySound` with `SND_MEMORY` and `SND_ASYNC`, looping every 10 seconds.

---

## License

This project is licensed under the `MIT` license.

---

## Disclaimer

This software is provided for educational and entertainment purposes only. Use at your own risk. The author is not responsible for any damage or loss caused by this software.
