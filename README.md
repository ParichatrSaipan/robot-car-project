# robot-car-project

This project is a robot car control system using RESTful API with Flask. The Raspberry Pi receives data from the ESP8266 via Serial communication and includes a Web Application for controlling the robot's movement, developed using React for the Frontend and Flask for the Backend.

## System Diagram
![image](/readme-picture/system-diagram.png)

## System Overview

- **User**:
    - Users can send commands through the Web Application accessible via Local Network, which connects to the Raspberry Pi that acts as the robot controller
    - Can control the robot's movement direction in real-time through the React-designed UI

- **Web Application**:
    - **React**: Used to develop the Frontend of the Web Application to create an easy-to-use UI with real-time data display from WebSocket
    - **Node.js**: Used as the Backend server of the application, managing user commands and communicating with Raspberry Pi through REST API
    - **WebSocket (WSS)**: For real-time video streaming from the camera on the robot to the web application, allowing users to monitor live video while controlling the robot

- **Raspberry Pi (Upper Level)**:
    - **Flask REST API**: Raspberry Pi acts as the main controller, using Flask to create a REST API for receiving commands from the Web Application and forwarding them to ESP8266 via Serial Communication
    - **WebSocket**: Raspberry Pi also sends real-time video signals from the WebCam back to the Web Application so users can monitor the robot's status

- **ESP8266 (Lower Level)**:
    - ESP8266 receives control commands from Raspberry Pi via Serial and converts commands into control signals to send to the L298N motor driver to control the motors

- **Motor Driver (L298N)**:
    - L298N Motor Driver controls the left and right motors using control signals from ESP8266 to change motor direction, such as moving forward, reversing, or stopping

- **Motors**:
    - The left and right motors move according to signals from the motor driver, allowing the robot to change direction and move according to specified commands

- **WebCam**:
    - WebCam connects to Raspberry Pi to record and stream live video to the Web Application through WebSocket, allowing users to monitor the robot's status in real-time

## System Summary

This system operates through a Local Network connection. Control commands from the Web Application developed with React and Node.js are sent via REST API to the Raspberry Pi, which forwards commands to the ESP8266 via Serial Communication using RX and TX pins. The ESP8266 then sends control signals to the motor driver and motors. Meanwhile, live video from the WebCam is streamed back to the Web Application through WebSocket, allowing users to see the robot's operation in real-time.

---

### Setting Up the System on Raspberry Pi 4

For additional setup steps for this project, see [Backend README.md](/back-end/README.md)

### Using ESP Code on ESP8266

For usage details and code development for ESP, see [ESP Code README.md](/esp-code/README.md)

### Setting Up Web Application on Raspberry Pi 4

For setup steps and usage for the Web Application, see [Web Application README.md](/robot-webapp/README.md)

---




