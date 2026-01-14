# Autonomous-Vehicle-Speed-Control-System-using-V2V-Communication
A GPS-integrated autonomous speed control system using the ATmega8 microcontroller. It automatically enforces speed limits by comparing real-time coordinates with pre-defined zone maps. Features include NMEA data parsing, PWM-based motor governance via an ESC, and a Hall Effect sensor feedback loop for precise speed regulation.

# Autonomous Vehicle Speed Control System (GPS-Based)

This project implements an electronic speed governor using the ATmega8 microcontroller. It is designed to automatically restrict a vehicle's speed when entering specific geographical zones (e.g., school or construction zones) by utilizing GPS data and closed-loop feedback.

## 🕹 System Functionality
The system monitors the vehicle's position via a **GTPA006 GPS receiver**. When the coordinates match a restricted zone stored in the MCU's memory, the controller overrides the driver's PWM input to the **Electronic Speed Controller (ESC)**, ensuring the vehicle does not exceed the legal limit.



## 🛠 Hardware Architecture
- **Microcontroller:** ATmega8 (AVR RISC architecture).
- **Positioning:** GTPA006 GPS Module (9600bps NMEA output).
- **Feedback:** Hall Effect Sensor for real-time RPM/Speed calculation.
- **Actuation:** Electronic Speed Controller (ESC) for DC Motor PWM management.



## 🛰 Zone Detection Logic
The system defines zones as coordinate squares. The MCU constantly parses the **$GPRMC** NMEA sentence to extract Latitude and Longitude.

```c
// Example logic for Zone Check
if (currentLat >= ZoneStartLat && currentLat <= ZoneEndLat) {
    speed_limit = ZONE_SPEED;
}
