# xbee-arduino
This is an Arduino library for communicating with XBees in API mode, with support for both Series 1 (802.15.4) and Series 2 (ZB Pro/ZNet). This library Includes support for the majority of packet types, including: TX/RX, AT Command, Remote AT, I/O Samples and Modem Status.
_This was originally on googlecode and now github. I will attempt to keep both repos in sync. See https://code.google.com/p/xbee-arduino/ for original documentation._ The [wiki](https://github.com/andrewrapp/xbee-arduino/wiki) of this repo is under updation.

**Note**: This software requires API mode, by setting AP=2. If you are using Series 2 XBee, you'll need to install API Firmware with [X-CTU](http://www.digi.com/support/productdetail?pid=3352&osvid=57&type=utilities) (Series 2 are manufactured with with AT firmware), then set AP=2. This software will not work correctly with AP=1 Refer to [XBeeConfiguration](http://code.google.com/p/xbee-api/wiki/XBeeConfiguration) and [WhyApiMode](http://code.google.com/p/xbee-api/wiki/WhyApiMode) for more info.

# Documentation
Doxygen API documentation is available in the downloads. Unfortunately it is not available online anymore as Git does not support the html mime type as Subversion does

# Example
I have created several sketches of sending/receiving packets with Series 1 and 2 XBee radios. You can find these in the [examples](https://github.com/andrewrapp/xbee-arduino/tree/master/examples) folder. Here's an example of sending a packet with a Series 2 radio:

    // Create an XBee object at the top of your sketch
    XBee xbee = XBee();

    // Start the serial port
    Serial.begin(9600);
    // Tell XBee to use Hardware Serial. It's also possible to use SoftwareSerial
    xbee.setSerial(Serial);

    // Create an array for holding the data you want to send.
    uint8_t payload[] = { 'H', 'i' };

    // Specify the address of the remote XBee (this is the SH + SL)
    XBeeAddress64 addr64 = XBeeAddress64(0x0013a200, 0x403e0f30);

    // Create a TX Request
    ZBTxRequest zbTx = ZBTxRequest(addr64, payload, sizeof(payload));

    // Send your request
    xbee.send(zbTx);

See the examples folder for the full source. There are more examples in the download.

See the [XBee API](http://code.google.com/p/xbee-api) project for Arduino < - > Computer communication.

To add XBee support to a new sketch, add "#include <XBee.h>" (without quotes) to the top of your sketch. You can also add it by selecting the "sketch" menu, and choosing "Import Library->XBee".

# Learning/Books
If you want to learn more about Arduino and XBee, check out these books:
* Wireless Sensor Networks: with ZigBee, XBee, Arduino, and Processing (Available in Kindle)
* Programming Arduino Getting Started with Sketches
* Making Things Talk
* Getting Started with Arduino (Make: Projects (Available in Kindle)
* Arduino Cookbook (Oreilly Cookbooks) (Available in Kindle)

# Installation
**Arduino 16 (or earlier):**

Download the zip file, extract and copy the XBee folder to ARDUINO_HOME/hardware/libraries If you are upgrading from a previous version, be sure to delete XBee.o

**Arduino 17 (or later):**

Determine the location of your sketchbook by selecting "preferences" on the Arduino menu. Create a "libraries" folder in your sketchbook and unzip the download there. See [this](http://arduino.cc/blog/?p=313) for more information.

# Uploading Sketches

The Arduino has only one serial port which must be connected to USB (FTDI) for uploading sketches and to the XBee for running sketches. The Arduino XBee Shield provides a set of jumpers to direct Serial communication to either the USB (Arduino IDE) or the XBee. When using the XBee Shield you will need to place both the jumpers in the USB position prior to uploading your sketch. Then after a successful upload, place the jumpers in the "XBEE" position to run your sketch. Always remember to power off the Arduino before moving the jumpers.

# Configuration
To use this library your XBee must be configured in API mode (AP=2). Take a look at [this](http://code.google.com/p/xbee-api/wiki/XBeeConfiguration) for information on configuring your radios to form a network.

# Other Micros
Not using Arduino? It should be easy to port this library to any microcontroller that supports C++ and serial available/read/write/flush. The only other dependency is the millis() function for milliseconds.

# Support
Please report any bugs on the [Issue Tracker](https://github.com/andrewrapp/xbee-arduino/issues).

# Questions/Feedback
Questions about this project should be posted to http://groups.google.com/group/xbee-api?pli=1 Be sure to provide as much detail as possible (e.g. what radios s1 or s2, firmware versions, configuration and code).

# Consulting/Commercial Licenses
I'm available for consulting to assist businesses or entrepreneurs that need help getting their projects up and running. I can also provide a commercial license for situations where you need to distribute code to clients/third parties that would otherwise conflict with GPL. For these matters I can be contacted at andrew.rapp [at] gmail.

# Support XBee Development
I typically don't like donate buttons since they can have a tendency to induce guilt. No one should ever feel obligated to donate, however if you'd like to it will be certainly appreciated and allow me to focus more time on the project. [Donate](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=VTJ7MEXNLZMGJ)
