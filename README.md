# Game SIGINT

![Version](https://img.shields.io/badge/version-1.2-2ea44f)
![Platform](https://img.shields.io/badge/platform-Windows%2010%2F11%20x64-0078D6)
![C++17](https://img.shields.io/badge/C%2B%2B-17-00599C?logo=cplusplus&logoColor=white)
![Dear ImGui](https://img.shields.io/badge/Dear%20ImGui-1.91.9b-4b6584)
![Three.js](https://img.shields.io/badge/Three.js-r160-000000?logo=threedotjs&logoColor=white)
![Direct3D 11](https://img.shields.io/badge/Direct3D-11-5E5E5E)
![WebView2](https://img.shields.io/badge/WebView2-runtime-0C59A4)
![MinGW-w64](https://img.shields.io/badge/build-MSYS2%20MinGW--w64%20GCC-7B3F9E)
![PowerShell](https://img.shields.io/badge/script-PowerShell-5391FE)
![Hamlib](https://img.shields.io/badge/Hamlib-rotctld%20%7C%20rigctld-8a6d3b)
![Languages](https://img.shields.io/badge/languages-EN%20%7C%20ID%20%7C%20JA-c0392b)

**An 8-bit flavoured signals intelligence (SIGINT) simulation in a single `.exe`.**
Created by **Octacons / YD1RUH**.

This is the developer README for the source folder. The public release page is
`release/repo/README.md`.

![The SIGINT room](release/repo/screenshots/01-room.png)

## About the game

You are the operator in the SIGINT room: four monitors, a cup of coffee, lo-fi music and
a cat that now and then walks across the desk. Read the briefing, build the RF chain (SDR,
antenna, cable, LNA), sweep the spectrum, identify and demodulate the signal, break the
cipher, locate the transmitter and report to command. Every attempt is randomised.

All operations, agencies, satellites and data are fictional and made for learning.
Intercepting communications without permission is against the law.

## Screenshots

| Intelligence briefing | Rig building and routing |
| --- | --- |
| ![Briefing](release/repo/screenshots/02-briefing.png) | ![Rig](release/repo/screenshots/03-rig.png) |
| **Spectrum sweep** | **Demodulator** |
| ![Sweep](release/repo/screenshots/04-sweep.png) | ![Demodulator](release/repo/screenshots/05-demodulator.png) |
| **Cryptanalysis** | **Direction finding** |
| ![Cryptanalysis](release/repo/screenshots/06-cryptanalysis.png) | ![Direction finding](release/repo/screenshots/07-direction-finding.png) |
| **Satellite tracking** | **Report to command** |
| ![Satellite](release/repo/screenshots/08-satellite.png) | ![Report](release/repo/screenshots/09-report.png) |
| **Training briefcase (Japanese)** | **About** |
| ![Briefcase](release/repo/screenshots/10-briefcase-ja.png) | ![About](release/repo/screenshots/11-about.png) |

## Operations

| Code | Target | Analysis |
| --- | --- | --- |
| OP-01 | VHF jammer | Jammer type |
| OP-02 | HF letter broadcast | Caesar |
| OP-03 | Rogue BTS | Traffic analysis |
| OP-04 | GPS spoofing | Proof of spoofing |
| OP-05 | X-band radar | ELINT library |
| OP-06 | FSK data burst | Vigenere |
| OP-07 | Drone telemetry | XOR with known plaintext |
| OP-08 | HF Morse | Rail fence and Caesar |
| OP-09 | GEO satellite, L-band | Unauthorised transponder use |
| OP-10 | LEO satellite, 437 MHz | Vigenere |

## Controls

| Key / click | Action |
| --- | --- |
| `1` `2` `3` `4` or click a monitor | SDR, Demodulator, Geospatial, Email |
| `5` or click the briefcase | Training modules |
| `Esc` | Back to the room |
| `ID` `EN` `日本` | Change language |
| Click the coffee / "Drink coffee" | Restore focus |
| Click the radio / "Lo-fi", `<<` `>>` | Music on or off, change track |
| "Music volume", "Font size" | Sound and display settings |
| Click the SDR rack | Build the rig |
| Click the cat | Pet the cat |
| Click or drag on the demodulator FFT | Set the filter width; mouse wheel zooms |
| "SDR gain", "Sample rate" | Gain affects SNR; sample rate sets how fast readings refresh |
| "Abort mission" (Email) | Cancel the active mission |

## Requirements

- 64-bit Windows 10 or 11.
- Microsoft Edge WebView2 Runtime (included in Windows 11).
- Japanese text uses a Japanese font that ships with Windows.

The game writes `WebView2Loader.dll` and its cache to `%LOCALAPPDATA%\SigintGame`.
Progress is not saved.

## Real hardware (optional)

The "Real hardware (Hamlib)" panel can connect to `rotctld` (port 4533) and `rigctld`, or to
SDR++ / gqrx remote control. Nothing connects until you press "Connect". The rotator moves
only when allowed and time is x1, and receives a stop command on disconnect. This feature
has not been tested with real hardware. Make sure the antenna area is clear.

## Building from source

Requires [MSYS2](https://www.msys2.org/) with the `mingw-w64-ucrt-x86_64-gcc` package,
`git` and PowerShell.

```powershell
powershell -ExecutionPolicy Bypass -File .\build.ps1      # output: dist\SIGINT.exe
powershell -ExecutionPolicy Bypass -File .\package.ps1    # output: dist\SIGINT-v1.2-win64.zip
```

If MSYS2 is not in `C:\msys64`, add `-Mingw <path>\ucrt64\bin`. The build downloads Dear
ImGui, the WebView2 SDK and Three.js, runs the tests, then links everything. It also needs
`sruput.mp3` in the project folder.

## Layout

| Path | Contents |
| --- | --- |
| `src/main.cpp` | Win32 window, Direct3D 11, WebView2 host |
| `src/ui.h`, `src/ui_sat.h` | Dear ImGui screens |
| `src/game.h` | Game rules |
| `src/missions.h`, `src/variant.h` | Mission data and randomisation |
| `src/crypto.h`, `src/orbit.h` | Classic ciphers and satellite orbits |
| `src/net.h` | Optional Hamlib client |
| `src/content.h` | Training modules and About text |
| `web/room.html` | 3D room, audio, music |
| `tests/test_game.cpp` | Checks that every mission can be solved |
| `release/` | Files for the public binary release |

## Credits

Game by **Octacons / YD1RUH**. Copyright 2026. Third-party components and the Natural Earth
map data are listed in [THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt).

73 de YD1RUH
