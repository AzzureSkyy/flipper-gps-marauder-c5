# GPS NMEA for ESP32-C5 Marauder board

Fork of `gps_nmea` (xMasterX / ezod) configured to use the GPS built into an
ESP32-C5 board running ESP32 Marauder firmware, instead of a bare GPS module.

How it works
- Flipper talks to the Marauder over the GPIO UART (pins 13 TX / 14 RX) at 115200
  (the Marauder CLI default). Same wiring/connection the Marauder Companion app uses.
- On start the app sends `stopscan` then `nmea`; Marauder streams raw NMEA from its
  onboard GPS and this app parses it with minmea, same display as the original.
- On exit it sends `stopscan` so the board returns to the normal CLI.

Controls (unchanged layout)
- OK: toggle backlight
- Long Up: cycle baud rate (default 115200)
- Long Right: cycle speed unit
- Long Down: re-send `stopscan` + `nmea` (restart the GPS stream)
- Back: exit

Build: run `ufbt` in `flipper_app/`. Output: `flipper_app/dist/gps_nmea_marauder.fap`
-> copy to `SD:/apps/GPIO/`.
