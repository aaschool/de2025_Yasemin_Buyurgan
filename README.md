# Print Center Queue Counter (AI-Based People Counting)

## Project Overview
This project provides a **real-time queue counter** for the Architectural Association **Print Center**, using an **AI-based people counting camera (ESP32-CAM with TensorFlow Lite)** to detect the number of people in the queue. The system consists of:
- **ESP32-CAM with AI-based object detection** to count people in the queue.
- **A Node.js backend** to process and store queue data.
- **A p5.js frontend** (widget & UI) to display queue updates to users in real-time.

---

## Project Structure
```
print-center-queue
   frontend/       # p5.js frontend
   backend/        # Node.js backend
   arduino/        # Arduino sketch for ESP32-CAM AI People Counting
   README.md       # This documentation file
```

---

## Required Components
### **Hardware Components**
  **ESP32-CAM** – AI-based people counting camera (Edge Processing).  
  **Power Source** – ESP32-CAM requires 5V power.  
  **WiFi Network** – Required for ESP32-CAM to send data to the backend.  

### **Software Requirements**
  **Arduino IDE** – To flash ESP32-CAM firmware.  
  **Node.js (Backend Server)** – Processes queue data and serves it to the frontend.  
  **p5.js (Frontend UI)** – Displays queue count live.  

---

## Required Libraries

### **p5.js (Frontend UI)**
- [`p5.serialport`](https://github.com/p5-serial/p5.serialport) → Serial communication with Arduino.
- [`p5.dom`](https://p5js.org/reference/#/libraries/p5.dom) → UI components like buttons, sliders.
- [`p5.sound`](https://p5js.org/reference/#/libraries/p5.sound) → Sound alerts when queue updates.
- [`socket.io-client`](https://socket.io/docs/v4/client-api/) → WebSockets for real-time queue updates.

### **Node.js (Backend Server)**
- [`express`](https://www.npmjs.com/package/express) → Handles HTTP requests.
- [`socket.io`](https://www.npmjs.com/package/socket.io) → WebSockets for real-time updates.
- [`body-parser`](https://www.npmjs.com/package/body-parser) → Parses incoming queue data.
- [`cors`](https://www.npmjs.com/package/cors) → Allows cross-origin requests from frontend.

### **Arduino (ESP32-CAM AI People Counting)**
- [`WiFi`](https://www.arduino.cc/en/Reference/WiFi) → Connects ESP32 to the internet.
- [`HTTPClient`](https://www.arduino.cc/reference/en/libraries/httpclient/) → Sends queue data to backend.
- [`esp_camera`](https://github.com/espressif/esp32-camera) → Enables ESP32-CAM to capture images.
- [`ArduinoJson`](https://arduinojson.org/) → Formats queue data as JSON.
- **TensorFlow Lite** → AI-based person detection.

---

## How the System Works

### **ESP32-CAM (Arduino Sketch - AI People Counting)**
- Captures a frame using the camera.
- Uses **TensorFlow Lite** to detect the number of people in the queue.
- Sends the queue count as a **JSON request to the backend** every 5 seconds.

### **Node.js Backend (Server)**
- Receives **queue count** from ESP32-CAM.
- Stores queue history in **MongoDB (Optional)**.
- Uses **WebSockets** to send live updates to the frontend.

### **p5.js Frontend (Queue Counter UI)**
- Connects to the backend via **WebSockets**.
- Displays real-time queue count.
- Allows toggling **notifications, sound alerts, and vibration**.

---
