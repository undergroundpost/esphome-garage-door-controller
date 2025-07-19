# ESPHome Garage Door Controller

A simple and reliable garage door controller using ESPHome and an ESP8266 (D1 Mini) that integrates with Home Assistant.

## Features

- **Remote Control**: Open/close garage door from Home Assistant
- **Status Monitoring**: Real-time door position feedback
- **WiFi Diagnostics**: Monitor signal strength
- **Fallback Access**: Captive portal if WiFi fails
- **Safety**: Debounced sensor inputs to prevent false triggers

## Hardware Requirements

- ESP8266 D1 Mini (or compatible)
- Reed switch or magnetic sensor for door position
- 5V relay module (for triggering garage door opener)
- Connecting wires
- Power supply (5V recommended)

## Wiring

- **GPIO14**: Door position sensor (reed switch) - connect between GPIO14 and GND
- **GPIO5**: Relay control pin - connects to relay IN pin
- **5V/VCC**: Power the relay module
- **GND**: Common ground for all components

## Installation

1. **Clone this repository**
   ```bash
   git clone https://github.com/undergroundpost/esphome-garage-door-controller.git
   cd esphome-garage-door-controller
   ```

2. **Configure secrets**
   ```bash
   cp secrets.yaml.template secrets.yaml
   # Edit secrets.yaml with your actual credentials
   ```

3. **Install to ESP8266**
   ```bash
   esphome run garage-door.yaml
   ```

4. **Add to Home Assistant**
   - The device should auto-discover via the ESPHome integration
   - If not, go to Settings > Integrations > ESPHome > Add Integration

## Configuration

### Door Sensor Logic

The code assumes the sensor is:
- **CLOSED** when the sensor circuit is open (door closed)  
- **OPEN** when the sensor circuit is closed (door open)

If your sensor works oppositely, change `inverted: false` to `inverted: true` in the binary_sensor configuration.

### Relay Timing

The relay pulse duration is set to 1 second. Adjust the `delay` values if your garage door opener requires a different pulse length.

## Safety Considerations

- Test thoroughly before permanent installation
- Ensure proper electrical isolation
- Consider adding additional safety sensors (obstruction detection)
- Test the fallback hotspot functionality

## Troubleshooting

- **Door status incorrect**: Check sensor wiring and `inverted` setting
- **Door doesn't respond**: Verify relay wiring and timing
- **WiFi issues**: Check signal strength sensor values
- **Compilation errors**: Ensure ESPHome version compatibility

## License

This project is open source and available under the MIT License.
