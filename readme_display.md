# Water Quality Display System

This project consists of a real-time water quality parameter display website and ESP32 code that sends simulated water quality data (pH, Turbidity, TDS) over WiFi. The system is designed for display purposes in science exhibitions, allowing viewers to see the water quality parameters without any control elements.

## System Components

1. **Display Website**: A clean, minimalist web interface that shows water quality parameters with color-coded sections
2. **ESP32 Sender**: ESP32 code that generates and sends simulated water quality data to the display website

## Display Website Features

- Real-time display of pH, Turbidity, and TDS values
- Color-coded sections: Blue for pH, Green for Turbidity, Orange for TDS
- Large, easy-to-read values with appropriate units
- Connection status indicator
- Last update timestamp
- Display-only interface with no control elements

## ESP32 Sender Features

- Connects to WiFi network
- Generates simulated water quality values:
  - pH (0.0 to 14.0)
  - Turbidity (1 to 500 NTU)
  - TDS (10 to 2000 ppm)
- Sends data to the display website using WebSockets or HTTP POST
- Configurable update interval

## Setup Instructions

### 1. ESP32 Setup

1. **Install Required Libraries** in Arduino IDE:
   - Go to Sketch > Include Library > Manage Libraries
   - Install the following libraries:
     - WebSocketsServer
     - ESPAsyncWebServer
     - AsyncTCP
     - SPIFFS

2. **Configure WiFi Settings**:
   - Open `main.ino` in Arduino IDE
   - Update the WiFi credentials:
     ```cpp
     const char* ssid = "YourWiFiSSID";
     const char* password = "YourWiFiPassword";
     ```
   - Update the web display IP address:
     ```cpp
     const char* webDisplayIP = "192.168.1.100"; // IP address of the computer running the display website
     ```

3. **Upload Code to ESP32**:
   - Connect your ESP32 to your computer
   - Select the correct board and port in Arduino IDE
   - Click Upload
   - Open Serial Monitor (115200 baud) to verify connection

### 2. Display Website Setup

#### Option 1: Simple Local Setup

1. Save the HTML file to your computer
2. Open the file directly in a modern web browser (Chrome, Firefox, Edge, etc.)
3. Note: For this method, use the WebSocket communication mode in the ESP32 code

#### Option 2: Local Web Server Setup (Recommended)

1. **Using Python's built-in HTTP server**:
   ```
   # Navigate to the directory containing the HTML file
   cd /path/to/folder
   
   # Start a simple HTTP server
   python -m http.server 80
   ```

2. **Using Node.js**:
   ```
   # Install http-server globally
   npm install -g http-server
   
   # Navigate to the directory containing the HTML file
   cd /path/to/folder
   
   # Start the server
   http-server -p 80
   ```

3. Open a web browser and navigate to `http://localhost` or `http://127.0.0.1`

#### Option 3: Host on a Web Server

For more permanent installations, you can host the HTML file on a web server like Apache or Nginx.

## Connecting the Components

1. Ensure both the computer running the display website and the ESP32 are on the same WiFi network
2. The ESP32 will automatically send data to the display website using the configured IP address
3. The display website will show "Connected" when it starts receiving data

## Troubleshooting

- **ESP32 not connecting to WiFi**:
  - Check WiFi credentials
  - Ensure the WiFi signal is strong enough where the ESP32 is located
  - Verify the WiFi network supports ESP32 connections (some networks restrict IoT devices)

- **Display website not receiving data**:
  - Check that the ESP32 and computer are on the same network
  - Verify the ESP32 has the correct IP address for the computer running the display website
  - Check if any firewalls are blocking connections
  - Try restarting both the ESP32 and the web server

- **Values not updating on the display**:
  - Check the serial monitor on the ESP32 to see if it's sending data
  - Verify the WebSocket connection in the browser's developer tools console
  - Try refreshing the page

## Customization

### Changing Update Frequency

To change how often the ESP32 sends new data:
```cpp
// Update interval (milliseconds)
const int updateInterval = 5000; // Adjust this value (in milliseconds)
```

### Changing Simulation Patterns

The ESP32 code includes two options for simulating values:
1. Random fluctuations (default)
2. Patterned changes (commented out)

To use patterned changes instead of random fluctuations, uncomment this line in `updateSimulatedValues()`:
```cpp
// updatePatternedValues();
```

### Customizing the Display

The display website uses standard HTML, CSS, and JavaScript. You can modify:
- Colors by changing the CSS variables at the top
- Layout by adjusting the grid and card styles
- Fonts and sizes to match your exhibition needs

## License

This project is provided for educational purposes. Feel free to modify and use it for your science exhibition or educational needs.
