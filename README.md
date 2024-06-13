# YOLOv8 Dog Pose Detection

## Introduction

This repository contains a custom YOLOv8 model for detecting dog poses in videos. Additionally, it includes an ESP8266-based project for identifying and sending IP addresses to a backend server. The ESP8266 device connects to predefined WiFi networks, scans for available networks, stores network information in EEPROM, and sends IP address data along with the floor number (based on the IP) to the backend server.

## Files

- `dog_custom.ipynb`: Jupyter notebook for training and inference.
- `True_Vid.mp4`: Sample input video.
- `outputs/`: Directory for output videos with detected poses.
- `runs/detect/train/weights/best.pt`: Trained model weights.
- `esp8266_ip_sender.ino`: Arduino sketch for the ESP8266 IP Address Identifier and Sender.

## Requirements

For YOLOv8 Dog Pose Detection:
- Python 3.6+
- PyTorch
- OpenCV
- NumPy
- Matplotlib
- Pillow
- YOLOv5 utils and models

For ESP8266 IP Address Identifier and Sender:
- Arduino IDE
- ESP8266 Board Package
- ESP8266WiFi library
- ESP8266HTTPClient library
- ArduinoJson library
- EEPROM library

## Usage

### YOLOv8 Dog Pose Detection

1. Clone the repository:
    ```bash
    git clone https://github.com/akhil99558/Pet_Management
    cd Pet_Management
    ```

2. Install the required Python packages:
    ```bash
    pip install -r requirements.txt
    ```

3. Run the Jupyter notebook `dog_custom.ipynb` for training and inference.

### ESP8266 IP Address Identifier and Sender

1. Open the `esp8266_ip_sender.ino` file in the Arduino IDE.

2. Configure WiFi credentials:
    ```cpp
    WifiCredentials knownNetworks[] = {
      {"SSID1", "password1"},
      {"SSID2", "password2"},
      {"SSID3", "password3"}
    };
    ```

3. Configure IP to floor mapping:
    ```cpp
    std::map<String, int> ipFloorMap = {
      {"192.168.1.100", 1},
      {"192.168.1.101", 2},
      {"192.168.1.102", 3}
    };
    ```

4. Upload the sketch to your ESP8266.

## Functional Overview

### YOLOv8 Dog Pose Detection

- **Training and Inference**: Use the `dog_custom.ipynb` notebook to train the YOLOv8 model on custom dog pose datasets and perform inference on videos.

### ESP8266 IP Address Identifier and Sender

- **setup()**: Initializes serial communication, begins EEPROM, and connects to known WiFi networks.
- **loop()**: Checks WiFi connection status, sends IP address data to the server if connected, and scans/stores networks if not connected.
- **connectToKnownNetwork()**: Scans and connects to known networks.
- **scanAndStoreNetworks()**: Scans and stores network information in EEPROM.
- **sendConnectedIP()**: Sends the current IP address and floor number to the backend server.
- **sendStoredData()**: Sends stored network information from EEPROM to the backend server.

## Serial Monitor Output

Use the Serial Monitor in the Arduino IDE (set to 115200 baud) to view debug output, including connection status, scanned networks, and responses from the backend server.

## Backend Server

The backend server URL is defined as:
```cpp
const String serverName = "http://backend.santhosh-toorpu.workers.dev/api/v1/sensor/data";
