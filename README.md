# Esp8266_deauther


![image](https://github.com/vasanthkumarch/Esp8266_deauther/assets/36288975/b627a1ad-4f7e-46f6-8879-87969de441b8)

Password
The password for pwned is deauther

About this Project
This firmware allows you to easily perform a variety of actions to test 802.11 networks using an ESP8266. It's also a great project for learning about WiFi, microcontrollers, Arduino, hacking and electronics/programming in general.

The deauthentication attack is the main feature, which can be used to disconnect devices from their WiFi network.
Although this denial-of-service attack is nothing new, a lot of devices are still vulnerable to it. Luckily this is slowly changing with more WiFi 6 enabled devices being used. But a lot of outdated WiFi devices remain in place, for example in cheap IoT hardware. With an ESP8266 Deauther, you can easily test this attack on your 2.4GHz WiFi network/devices and see whether it's successful or not. And if it is, you know you should upgrade your network.

Disclaimer
This project is a proof of concept for testing and educational purposes.
Neither the ESP8266, nor its SDK was meant or built for such purposes. Bugs can occur!

Use it only against your own networks and devices!
Please check the legal regulations in your country before using it.
I don't take any responsibility for what you do with this program.



Have you ever thought about jamming the Wi-Fi connection network? Now days Wi-Fi password hacking is very common, so by jamming the Wi-Fi network you can block or jam any Wi-Fi connection, and no one is able to connect to that Wi-Fi network even after knowing the password. This can be done with a tiny Microcontroller ESP12E, which is also referred as Wi-Fi module or NodeMCU. If you are new to this small but powerful chip, then go through Getting started with ESP12 article. ESP is very popular for Wi-Fi tricks like creating a fake Wi-Fi network, serving your own page to steals someone’s password, block the Wi-Fi network etc. Even ESPs are being sold, with all the software flashed on them for doing these tricks, you just need to Plug and Play. But here we are creating our own Wi-Fi jammer.

Technically, we are not making a jammer but a Deauther. There is a small difference between these. A Jammer sends noise signals to the Wi-Fi spectrum (2.4GHz) thus disturbing original Wi-Fi frequency spectrum. While a Deauther sends packets to interfere with your Wi-Fi signals thus disrupting the normal working of your Wi-Fi router.  It behaves like a jammer.

There is a Wi-Fi protocol called 802.11 which act as a deauthentication frame. This is used to safely disconnect all the users connected with the router. To disconnect any device from some Wi-Fi network, it is not important to know the password or to be in the network, you just need mac address of the Wi-Fi router and client device and it is enough to be in its range of that Wi-Fi network.

Disclaimer: It is illegal to use jammer in the public areas without taking permission of govt. authority. This tutorial is just for educational purpose. Do it on your risk.

Two Methods to make Wi-Fi jammer with NodeMCU
There are plenty of available Codes or firmware to make NodeMCU as Wi-Fi jammer. You just need to burn the code or firmware into NodeMCU. Here we have selected two stable and easy methods, using which you can use NodeMCU to act as Wi-Fi jammer.

1. Uploading Jammer Arduino sketch into ESP12.

For this method we will use Arduino code and Library written by Spacehuhn and it is very long code so we will use this code to directly upload in our NodeMCU using Arduino IDE.

2. Uploading Wi-Fi Jammer firmware into ESP12 using ESP8266 flasher.

For this method we need Jammer firmware for NodeMCU which be downloaded from the given links:

ESP8266 flasher
Deauther Firmware – It is basically a .bin file .It is available for three NodeMCU versions depending on flash memory (1MB, 4MB and 512Kb). Download the version according to your board specification. In my case, board version is 1MB.
Download firmare for NodeMCU

Method 1: Uploading Jammer Sketch using Arduino IDE
Let’s start with uploading the Arduino code

Step 1:- Go to File -> Preferences in Arduino IDE and add this link http://arduino.esp8266.com/stable/package_esp8266com_index.json

to the Additional Boards Manager URLs and Click on OK.

Setting up preference for Arduino IDE

Close the Arduino IDE and Reopen it.

Step 2:- Click on Tools -> Board -> Board Manager. Search for ESP8266. You must select version 2.0.0. This code will work only for this version. If you have already installed another versions, remove it and install 2.0.0

Install ESP8266 in Arduino IDE

Step 3:- Again go to File -> Preferences and click the folder path under More preferences.

Step 4:- Now, open the packages -> esp8266 -> hardware -> esp8266- > 2.0.0 -> tools -> sdk -> include
and open the  user_interface.h file with the text editor.

Step 5:- Come to last line of the code and before #endif  and add these lines:

typedef void (**freedom_outside_cb__t)(uint8 status);
int wifi_register_send_pkt_freedom_cb(freedom_outside_cb_t cb);
void wifi_unregister_send_pkt_freedom__cb(void);
 int wifi_send_pkt_freedom(uint8 **buf, int len, bool sys_seq);
Then Save the file.

Step 6:- Extract the library that you have downloaded earlier and open it. Open esp8266_deauther-master -> esp8266_deauther -> esp8266_deauther.ino

This is the sketch which will be uploaded in the NodeMCU. Compile this sketch. If there is a error then you have to install these libraries:

ArduinoJson
ESP8266 OLED SSD1306
Adafruit NeoPixel
LinkedList
Now, your code is ready to upload. Connect NodeMCU to the PC, Choose NodeMCU esp-12E board from tools menu, choose the correct port and hit the upload button.

Running the NodeMCU Wi-Fi Jammer
Reset your ESP12 board after uploading the code and open the Serial Monitor.

You will see this information on serial monitor:

Running the NodeMCU Wi-Fi Jammer

Step 1:- Now, connect your laptop or smartphone with Access Point created by NodeMCU. Name of AP is “pwned” and password is “deauther” These are default name and password which you can see on serial monitor .

Step 2:- Open your browser and enter this address 192.168.4.1 .

You will see a warning, read it and click on I have read and understood

Opening ip in browser

Step 3:- After this you will see the window given below. Click on Scan APs to search for the WiFi networks available. Now, click on Reload.

Scan for Wi-fi availability

Step 4:- Click on the WiFi network which you want to Jam. You can choose more than one but it will make your NodeMCU unstable.

Click on the WiFi network which you want to Jam

Step 5:- Click on Attacks and you will see that you have chosen one target for attack. To start the Attack click on start and then Reload.

You have successfully jammed the network. To stop the attack click on stop button.

Click start to Attack on wifi network

Make a fake WiFi network
If you want to make fake WiFi networks i.e. Beacons. Click on SSIDs above and name the SSIDs as you want .Add and save it. Come back to Attacks menu and click on Start in front of Beacon.

Make a fake Wifi network

You can check in your mobile or PC that wifi name that you have created will be displayed but it will not connect with this fake network it is just a WiFi spam.
