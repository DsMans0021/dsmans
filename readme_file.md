# Water Quality Simulator for Science Exhibition

This project consists of a web-based control interface and ESP32 code that allow you to simulate and send water quality values (pH, Turbidity, TDS) to an Orphius Pico (ESP32) microcontroller over WiFi. This is designed for science exhibitions to demonstrate water quality monitoring without real sensors.

## Project Contents

- `index.html` - The web interface with sliders to control pH, Turbidity, and TDS values
- `main.ino` - ESP32 code that connects to WiFi and receives the simulated values

## Setup Instructions

### 1. ESP32 (Orphius Pico) Setup

1. **Install required libraries**:
   - Open Arduino IDE
   - Go to Tools > Manage Libraries...
   - Install the following libraries:
     - WiFi.h (included with ESP32 board)
     - WebServer.h (included with ESP32 board)
   - Optional: If using OLED, also install:
     - Adafruit_GFX
     - Adafruit_SSD1306

2. **Configure WiFi settings**:
   - Open `main.ino` in Arduino IDE
   - Locate the WiFi configuration section at the top:
     ```cpp
     const char* ssid = "YourWiFiSSID";      // Your WiFi network name
     const char* password = "YourWiFiPassword";  // Your WiFi password
     ```
   - Replace with your actual WiFi credentials

3. **Optional: Configure OLED display**:
   - If you have an OLED display connected to your ESP32, uncomment the OLED-related code sections
   - Make sure the I2C address matches your display (default is 0x3C)

4. **Optional: Configure LED pins**:
   - If you want to use LEDs as visual indicators, adjust the pin numbers:
     ```cpp
     const int LED_PH = 12;       // Blue LED for pH
     const int LED_TURBIDITY = 14; // Green LED for turbidity
     const int LED_TDS = 27;       // Orange/Yellow LED for TDS
     ```

5. **Upload to ESP32**:
   - Connect your ESP32 to your computer
   - Select the correct board (ESP32 Dev Module) and port
   - Click Upload
   - Open Serial Monitor at 115200 baud to see the device's IP address

6. **Note the IP address**:
   - When the ESP32 connects to WiFi, it will print its IP address to the Serial Monitor
   - You'll need this IP address to configure the web interface

### 2. Web Interface Setup

1. **Simple method (Local File)**:
   - Just open `index.html` in any modern web browser
   - This works for most cases and doesn't require additional software

2. **Using a local web server (optional but recommended)**:
   - For better reliability, you can use a local web server
   - Python simple server method:
     ```
     # Navigate to the directory containing index.html
     python -m http.server 8000
     ```
   - Then open `http://localhost:8000` in your browser

3. **Configure ESP32 connection**:
   - In the web interface, enter the ESP32's IP address (noted earlier)
   - The default port is 80, which typically doesn't need to be changed

## Usage Instructions

1. **Open the web interface** in your browser
2. **Adjust the sliders** to set the desired values:
   - pH (0.0 to 14.0)
   - Turbidity (1 to 500 NTU)
   - TDS (10 to 2000 ppm)
3. **Click "Send Values to Device"** to transmit the values to the ESP32
4. **Check the status message** to confirm successful transmission
5. **Verify on ESP32**:
   - The Serial Monitor will display the received values
   - If configured, LEDs will light up based on thresholds
   - If OLED is enabled, values will appear on the display

## Troubleshooting

- **Web interface can't connect to ESP32**:
  - Ensure both the computer and ESP32 are on the same WiFi network
  - Check that the IP address is entered correctly
  - Try pinging the ESP32 IP address to verify connectivity

- **ESP32 not connecting to WiFi**:
  - Double-check WiFi credentials
  - Ensure WiFi signal is strong enough
  - Reset the ESP32 and try again

- **Values not updating on ESP32**:
  - Check Serial Monitor for error messages
  - Ensure the ESP32 code is running correctly
  - Try restarting both the ESP32 and the web interface

## Customization

- **Adjusting slider ranges**:
  - Edit the `min`, `max`, and `step` attributes of the sliders in `index.html`
  - Update the validation ranges in the ESP32 code to match

- **Adding more parameters**:
  - Add new sliders to the HTML interface
  - Update the comma-separated format in both the JavaScript and ESP32 code
  - Add new variables to store and display the additional parameters

- **Changing the visual design**:
  - Modify the CSS styles in the `<style>` section of `index.html`
  - For different section colors, update the CSS variables at the top

## License

This project is provided for educational purposes. Feel free to modify and use it for your science exhibition needs.
