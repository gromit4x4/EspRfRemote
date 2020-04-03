# MercuryEspRfRemote
Sketch to use an ESP with Arduino as a RF remote for Mercury remote sockets set 350.115UK

Step 1:
install Arduino IDE

Step 2:
Add to File -> Preferences -> Additional Boards.. the url: http://arduino.esp8266.com/stable/package_esp8266com_index.json

Step 3:
Tools -> Boards Manager.. install ESP8266 by esp community

Step 4:
Connect your device prefferably WeMos and set serial port
And connect a 4433Mhz transmitter to pin D4 (or other you specify later in the web ui)

Step 5:
set ssid and password to your wifi crendentails

Step 6:
Upload sketch. Open Tools -> Serial Monitor with 115200 Baud rate

Step 7:
Successful connect will show ip in serial monitor
Use your browser to open the ip
http://<ip.of.the.device>

A simple UI will show up. You can control the parameters and the corresponding url that can be used to perform the action will be shown

--------------------------------------------------------------------------

The original code has been modified to suit Mercury remote sockets set 350.115UK

The Mercury sockets require the same preamble and ID code format but switch on/off differently.

Changes have been made to omit the on/off bit and channel select option as the Mercury sockets don't use them.
Mercury use a static on/off code and a unique ID for each socket.

The output is now Pin D4, t 187, ID, 1/0 for on/off.

To set several sockets select a different ID for each (increment or decrement the ID) and copy the resulting URL.
E.G: 

http://192.168.1.10/rf?D=4&t=187&id=28016&on=1 socket 1 on

http://192.168.1.10/rf?D=4&t=187&id=25018&on=1 socket 1 on

Or edit the included .html with your ESP device IP address and use to control several sockets from a browser 
(requires each socket to be paired with the transmitted code from the .html)

-----------------------------------------------------------------------------

If you have the means to capture your 433mhz remote codes, you can emulate the same code via http and use both remote control and browser to operate the same sockets.

A quirk of the original code is that the transmitted ID code gets inverted. To find the required code to transmit, first capture the remote on or off that you wish to emulate.

E.G.

Socket 1 On = Binary: 000101010101110100000011

Remove the last 4 bits: 00010101010111010000 - [0011] and convert the remaining 20 bits to decimal = 87504

Use the web UI of the ESP device to transmit the on signal with ID 87504 and again capture the transmitted code.

ESP transmission = Binary: 10111010101010000011

Again remove the last 4 bits: 1011101010101000 - [0011] and convert the remaining 20 bits to decimal = 47784

47784 is the ID we need to transmit to emulate the remote control.

Original code here: https://github.com/bitluni/EspRfRemote
