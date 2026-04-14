# etch-a-sketch-web

Browser viewer for the ESP32 Etch-a-Sketch WebSocket stream.

```
cd /Users/benjamin/Documents/CodingProjects/etch-a-sketch-main/etch-a-sketch-web
python3 -m http.server 8000
```

Open `http://localhost:8000/etch-a-sketch.html`, enter the ESP32 IP address,
and press `Connect`.

## WebSocket liveness

- The viewer connects to `ws://<ESP32_IP>/ws` using subprotocol
	`etchsketch.v1.json`.
- While connected, the browser sends `{"type":"heartbeat"}` every 2 seconds.
- The ESP32 should reply on the same socket with `{"type":"heartbeat_ack"}`.
- Any inbound WebSocket message counts as liveness.
- If no inbound message arrives for 6 seconds, the viewer marks the connection
	as `Disconnected` with the red status indicator.
- All terminal disconnect cases use the same user-facing status:
	`Disconnected`.
