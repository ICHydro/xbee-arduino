# xbee-arduino

## Changes to the original version

This project is a fork of the [xbee-arduino project by andrewrapp](https://github.com/andrewrapp/xbee-arduino), extending its funcionality to the [XBee Cellular 3G](https://www.digi.com/products/embedded-systems/digi-xbee/cellular-modems/digi-xbee-cellular-3g) modem. The major differences are:

* New classes and functions for the specific frame types to send and receive TCP, UDP, and SMS messages with the Cellular XBee.

* Using uint16_t instead of uint8_t types to store the variables related to the frame length, because the cellular XBee uses much longer framelengths to accommodate the transmission payload.

* Introducing `XBee` and `XBeeWithCallBaks` constructors in which the buffer length can be set by the user. In the original version the buffer length is hard-coded at 110 bytes, which is not sufficient for the larger payloads of the Cellular XBee.

## Basic usage

Here is the basic usage. More elaborate examples to come...

```cpp
// Using the httpbin example included in the Xbee Cellular 3G manual

char host[] = "httpbin.org";
uint32_t ip = 0x00000000;     // Change this for the ip address or use lookup
const uint16_t port = 0x50;   // port 80
uint8_t protocol = 1;         // TCP

const char getMsg[] = "GET /ip HTTP/1.1\r\nHost: httpbin.org\r\n\r\n";
uint8_t responsebuffer[2500];

XBeeWithCallbacks xbc(responsebuffer, sizeof(responsebuffer));
IPTxRequest ipRequest(ip, port, (uint8_t*)getMsg, sizeof(getMsg)-1);

ipRequest.setProtocol(protocol);

xbc.send(ipRequest);
```
## Acknowledgements


Many thanks to Isabella Mapstone for the coding work.

