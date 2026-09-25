# ESP32 Web Control Panel

A single-file, mobile-first web interface for driving an ESP32 (or ESP32-CAM) device over the local network. It exposes a four-direction control pad that sends HTTP requests to the device, making it suitable for pan/tilt camera mounts, small robots, or any firmware that exposes simple HTTP endpoints.

## Features

- Directional pad (up, down, left, right) with large touch targets
- Configurable device base URL, persisted in the browser with `localStorage`
- Request timeout handling and a live status line reporting success or failure
- Dark theme built on Bootstrap 5 and Bootstrap Icons
- No build step and no backend: a single `index.html`

## Device contract

Each button issues a `GET` request to the configured base URL (default `http://192.168.4.1`, the ESP32 soft-AP address):

| Button | Path |
| --- | --- |
| Up | `/up/cliked` |
| Down | `/down/cliked` |
| Left | `/left/clicked` |
| Right | `/right/clicked` |

The firmware on the ESP32 must register handlers for these paths. They are defined in a single object in the page script and can be renamed to match your firmware.

## Usage

1. Connect your phone or computer to the same network as the ESP32 (or to its access point).
2. Open `index.html` in a browser, or serve it from the ESP32 file system (SPIFFS or LittleFS).
3. Enter the device address in the URL field and press **Save**.
4. Use the directional buttons. The status line shows the result of each request.

If the page is served from a different origin than the device, the firmware must allow cross-origin requests (`Access-Control-Allow-Origin`).

## License

No license has been specified yet. Contact the author before reusing this code.
