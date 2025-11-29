# Robot Car Control with ESP8266

This project uses an ESP8266 microcontroller to control a robot car to move according to basic commands. The robot responds to Serial commands to move forward, reverse, turn left, turn right, and stop, using PWM for speed control and GPIO for direction control.

## Components

- **ESP8266**: Microcontroller for receiving commands and controlling motors
- **Motor Driver**: Controls the direction and speed of the robot wheels
- **DC Motors**: Drive the robot wheels
- **Serial Communication**: Receives movement commands from external sources

## Pin Configuration

- **Motor Direction Control Pins**:
    - `LEFTF1` (D6): Left motor forward
    - `LEFTF2` (D7): Left motor reverse
    - `RIGHTF1` (D8): Right motor forward
    - `RIGHTF2` (D0): Right motor reverse

- **PWM Speed Control Pins**:
    - `SPEED_A` (D3): Left motor speed control
    - `SPEED_B` (D4): Right motor speed control

## Features

1. **Direction Control**: Receives commands to move forward, reverse, turn left, turn right, and stop
2. **PWM Speed Control**: Speed set at 50% duty cycle
3. **Timeout Management**: Each movement lasts for 500 milliseconds to prevent continuous movement without new commands
4. **Command Parsing**: Receives commands via Serial and processes them to control movement

## Installation

1. Connect ESP8266 to the motor driver and motors according to the pin configuration above
2. Upload the code to ESP8266
3. Use a Serial Interface (e.g., Arduino Serial Monitor) to send commands

## Commands

Commands are sent via Serial and processed as follows:

- `forward`: Move robot forward for 500 milliseconds
- `reverse`: Move robot backward for 500 milliseconds
- `left`: Turn robot left for 500 milliseconds
- `right`: Turn robot right for 500 milliseconds
- `stop`: Stop robot immediately

## Serial Output Example

When the robot receives commands via Serial, it will display feedback in the Serial Monitor as follows:

    ```
    Moving Forward
    Timeout: Stopping Forward Movement
    Reversing
    Timeout: Stopping Reverse Movement
    Turning Left
    Timeout: Stopping Left Turn
    Turning Right
    Timeout: Stopping Right Turn
    Stopping
    ```

## Code Explanation

### Movement Functions

- **`startForward()`**: Sets pins to move robot forward and starts timer
- **`reverse()`**: Sets pins to move robot backward and starts timer
- **`moveLeft()`**: Sets pins to turn robot left and starts timer
- **`moveRight()`**: Sets pins to turn robot right and starts timer
- **`stop()`**: Stops all movement by setting motor pins to LOW

### Code Example

Each movement function uses `digitalWrite` to control motor direction and uses flags to track robot status:

```cpp
void startForward() {
    digitalWrite(LEFTF1, HIGH);
    digitalWrite(LEFTF2, LOW);
    digitalWrite(RIGHTF1, HIGH);
    digitalWrite(RIGHTF2, LOW);
    moveStartTime = millis();
    isMovingForward = true;
}
