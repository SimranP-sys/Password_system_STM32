# Password_system_2step_STM32
A two step verification password system using STM32 Nucleo board. The project consist of verifying authentication using 
1. A keypad based verification
2. Clap based verification

Two-Step Password System Using STM32L152RE

A two-step authentication system built with an **STM32L152RE Nucleo board**. The system combines a password entered through a custom 2×2 button keypad with sound-based verification using a microphone sensor.

The project demonstrates GPIO-based keypad scanning, OLED display control over I²C, and a simple sound-event authentication method using STM32 HAL drivers.

## Features

- Custom 2×2 matrix keypad made from four push buttons
- Row-column scanning to identify button presses
- Four-character password verification
- Password masking on the OLED display
- OLED prompts for each authentication stage
- Second-factor verification using a microphone sensor
- Clap detection requiring five detected claps
- Access-granted indication after successful verification
- Built with STM32CubeIDE and STM32 HAL libraries

## How It Works

The authentication process has two steps:

### Step 1: Password Verification

1. The OLED displays **“Enter Password”**.
2. The user enters a four-button sequence using the 2×2 keypad.
3. Each entered key is displayed as an asterisk (`*`) instead of showing the actual input.
4. The entered sequence is compared with the password stored in the firmware.
5. If the password is incorrect, the OLED displays **“Wrong!!”** and access is denied.

### Step 2: Sound Verification

1. If the password is correct, the OLED displays **“Step 2”**.
2. The microphone sensor monitors its digital output for detected sound events.
3. The current implementation uses claps as the sound event.
4. After five claps are detected, the system displays **“Access Granted!!”**.
5. The onboard LED is toggled as an indication while sound events are detected.

> **Note:** In the current prototype, access is indicated through the OLED and onboard LED. A relay, servo motor, solenoid, or electronic lock can be connected to the access-control output for a physical locking application.

## Components Used

- STM32L152RE Nucleo board
- Four push buttons for the 2×2 matrix keypad
- OLED display with I²C interface
- Digital microphone or sound sensor module
- Breadboard and jumper wires
- Resistors as required by the button and sensor circuits
- Optional: relay module, servo motor, solenoid lock, or electronic lock

## Software and Libraries

- STM32CubeIDE
- STM32 HAL library
- STM32L1 device support package
- SSD1306 OLED driver
- OLED font library
- C programming language

## Interface Summary

| Module | STM32 Interface / Signal | Purpose |
|---|---|---|
| OLED display | I²C1 | Displays prompts, password status, and access status |
| Keypad rows | GPIO outputs | Drives one keypad row at a time during scanning |
| Keypad columns | GPIO inputs | Detects the pressed button in the active row |
| Microphone sensor | PA9 | Reads the digital sound-event signal |
| Onboard LED | PA5 | Indicates detected sound events / access activity |

The exact keypad row and column aliases are defined in the STM32CubeMX-generated project files, such as `main.h`.

## Keypad Scanning

The four push buttons are arranged as a 2×2 matrix:

```text
        Column 1    Column 2
Row 1   Button 1    Button 2
Row 2   Button 3    Button 4
```

The firmware sets one row active at a time and reads the column inputs. This allows the STM32 to determine which button is pressed using four GPIO signals instead of requiring one GPIO pin per button.

Images






<img width="216" height="300" alt="img" src="https://github.com/user-attachments/assets/5a6a7129-555f-471a-8f9a-d6cf8ba59719" />




