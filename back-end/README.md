# Robot Control API

This project is a Flask-based API for controlling a robot car. The Raspberry Pi receives data from ESP8266 via Serial communication.

## Prerequisites

1. **Python**: Make sure you have Python installed on your system
2. **Flask**: Install Flask and other dependencies using `pip install -r requirements.txt` after cloning the repository

## Installation

1. **Clone the repository**:
    ```bash
    git clone https://github.com/saipanm/robot-car-project.git
    cd back-end
    ```

2. **Install dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

## Configuration

1. **Set up Serial connection**:
    - Make sure ESP8266 is connected to the correct Serial port of Raspberry Pi
    - Adjust the Serial port in the code if necessary:
      ```python
      ser = serial.Serial('/dev/serial0', 9600, timeout=1)  # Replace '/dev/serial0' with the correct port
      ```

## Running the API

1. **Create a bash file to start Flask API**:

    Create a file named `start.sh` and write the following code:

    ```bash
        export FLASK_APP=robot_control_api.py
        export FLASK_ENV=production
        gunicorn -w 4 -b 0.0.0.0:1212 robot_control_api:app
    ```
2. **Run API automatically using pm2 from bash file**:
    ```bash
    pm2 start start_api.sh
    ```


## API Endpoints

### 1. Move Robot

- **Endpoint**: `/api/move`
- **Method**: `POST`
- **Description**: Move the robot in a specified direction
- **Request Example**:
    ```json
    {
        "direction": "forward", "reverse", "left", "right", "stop"
    }
    ```
- **Response**:
    ```json
    {
        "status": "moving <direction>",
        "response": "<response from esp>"
    }
    ```

### 2. Check API Status and Serial Connection

- **Endpoint**: `/api/status`
- **Method**: `GET`
- **Description**: Check the status of the API and Serial connection
- **Response**:
    ```json
    {
        "status": "API is running",
        "serial_connection": "connected" , "disconnected"
    }
    ```

## Code Explanation

### Serial Communication

The **`send_command`** function sends commands to ESP8266 and waits for a response

 ```python
    def send_command(command):
        if ser and ser.is_open:
            ser.write((command + "\n").encode('utf-8'))  
            print(f"Sent to esp: {command}")

            response = ser.readline().decode('utf-8', errors='ignore').strip()
            if response:
                print(f"esp response: {response}")
                return response
            else:
                print("No response from esp.")
                return "No response"
        else:
            print("Error: Serial connection is not open.")
            return "No connection"
  ```

### API Resources

- **MoveResource**: Handles POST requests to control robot movement

  ```python
        class MoveResource(Resource):
            def post(self):

                data = request.json
                direction = data.get("direction")

                if not direction:
                    return {"error": "No direction provided"}, 400

                valid_directions = ["forward", "reverse", "left", "right", "stop"]
                if direction not in valid_directions:
                    return {"error": "Invalid direction"}, 400

                response = send_command(direction)
                return {"status": f"moving {direction}", "response": response}

    ```

- **StatusResource**: Handles GET requests to check API status and Serial connection
    ```python
    class StatusResource(Resource):
        def get(self):
            connection_status = "connected" if ser and ser.is_open else "disconnected"
            return {"status": "API is running", "serial_connection": connection_status}
    ```
