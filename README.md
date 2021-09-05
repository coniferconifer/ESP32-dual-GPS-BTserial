# ESP32 dual GPS-BT-server with watch dog timer

By hooking up two multiGNSS GPS modules to ESP32, 
This program read NMEA from two GPS modules and averages latitude,longitude,height,number of satellites, hdop and course, then 
outputs NMEA to Bluetooth Serial Port Profile.

NMEA can be monitored by ESP32's USB serial port.

Only \$GNGGA and \$GNRMC are regenerated by this program.
Other \$??GSV , \$??GSA and \$??TXT of GPS2 are just relayed to the output. 
You can monitor how this works by u-center or other NMEA monitoring tools.

When Serial BT stalls , software watch dog timer reboots ESP32.

## Application 

![ataglance](https://github.com/coniferconifer/ESP32-dual-GPS-BTserial/blob/main/comparison2.png)
2dRMS(m) for Location and Height comparison

![system](https://github.com/coniferconifer/ESP32-dual-GPS-BTserial/blob/main/block.drawio.png)

![multiGNSS](https://github.com/coniferconifer/ESP32-dual-GPS-BTserial/blob/main/dualgps.jpg)

Use your external GPS module as Android's internal GPS.

Step1. Configure mock-location on Android.

Ref. https://eos-gnss.com/knowledge-base/configuring-mock-location-on-android-with-your-arrow-gnss-receiver

Step2. Run Lefebure NTRIP Client on Android to replace from Android phone's embeded GPS to your GPS.
No need to set up NTRIP server if your GPS module does not support RTK GPS.
 
Ref. https://play.google.com/store/apps/details?id=com.lefebure.ntripclient&hl=ja&gl=US


## How to wire your GPS module
https://shop.m5stack.com/products/mini-gps-bds-unit

GPS1 TX should be connected to GPIO_NUM_33 of ESP32

GPS2 TX should be connected to GPIO_NUM_16 of ESP32

LED with resister at GPIO_NUM_2 blinks every 2sec.

GPS used to test : M5stack GPS module (using AT6558) , connected by 9600bps serial.

AT6558 https://shop.m5stack.com/products/mini-gps-bds-unit

Android BT serial terminal: https://play.google.com/store/apps/details?id=de.kai_morich.serial_bluetooth_terminal&hl=ja&gl=US

Monitoring tool : "NMEA Monitor for windows" http://4river.a.la9.jp/gps/index.htm

"NMEA Monitor for windows" provides 2dRMS to see dual GPS has better accuracy or not. d2RMS is twice the distance root mean square radial, says 95% of data falls in this distance(m) from central value.

## Libraries 
TinyGPS+

Ref. http://arduiniana.org/libraries/tinygpsplus/

Bluetooth Serial Port Profile at ESP32

Ref. https://github.com/espressif/arduino-esp32/blob/master/libraries/BluetoothSerial/
      
## License

Copyright 2021(C) coniferconifer

MIT License

## single GPS BT serial
https://github.com/coniferconifer/ESP32-GPS-BTserial

## Misc
To observe the Sun flare , precise height from GNSS module is necessary.
Geospatial Information Authority of Japan observed GPS height anormaly
in Sep 8,2017 (JST) in Ref.  https://www.gsi.go.jp/denshi/denshi40001.html
 