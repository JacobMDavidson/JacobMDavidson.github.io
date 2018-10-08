---
layout: post
title: ComputerSMS Android and Desktop Applications
description: "I currently own a Moto X and looked forward to the Motorola Connect feature when it was first released. The promise of Motorola Connect was to allow SMS messaging via a Chrome browser plugin. Unfortunately, the delivered product fell well short of my expectations. Initialization was slow, messages weren't sent and received in a timely fashion, messages sent and received within Motorola Connect were not accessible in the messages app on my phone, and using the plugin meant that my messages were being stored on yet another server over which I have no control. Needless to say, I stopped using the Chrome browser plugin after my first experience. I needed to create a better solution for my personal needs."
modified: 2015-10-02
tags: [android, desktop, java, java desktop, java mobile]
comments: false
image:
  feature: android/computersms-banner.png
---

## Send SMS Messages from a Computer through an Android Phone

Using the [ComputerSMS Android application](https://github.com/JacobMDavidson/ComputerSMS) in conjunction with the [ComputerSMSServer Java desktop application](https://github.com/JacobMDavidson/ComputerSMSServer) will allow you to send and receive text messages through your Android phone using your computer. The Android phone and computer must be connected to the same local network.

#### Why were these applications developed?

I currently own a Moto X and looked forward to the Motorola Connect feature when it was first released. The promise of Motorola Connect was to allow SMS messaging via a Chrome browser plugin. Unfortunately, the delivered product fell well short of my expectations. Initialization was slow, messages weren't sent and received in a timely fashion, messages sent and received within Motorola Connect were not accessible in the messages app on my phone, and using the plugin meant that my messages were being stored on yet another server over which I have no control. Needless to say, I stopped using the Chrome browser plugin after my first experience.

***What were the essential features I desired?*** I simply wanted to access the SMS functionality of my phone through my computer when connected to the same local network. This would allow for easy messaging while charging my phone and could be easily expanded to notify me of any incoming calls.

A combination Android and desktop SMS messaging application would solve the glaring issues I experienced with Motorola Connect. All SMS activity would occur within the phone itself, requiring no additional servers and storing all message activity within the phone itself. Initialization would be much faster, and virtually no additional lag would be introduced in the sending and receiving of the messages. Not to mention, these applications would be fairly simple to create.

I created the ComputerSMS Android application and ComputerSMSServer Java desktop application to solve my problem, and I used this development opportunity to expand my knowledge of Multi-Cast DNS, Diffie-Hellman key exchanges, AES encryption, and XML serialization and parsing within Android.

#### Application Instructions:

1. Ensure both the computer and Android phone are connected to the same local area network.
2. Open the ComputerSMSServer desktop application and select *"Start"*.
3. Wait for the message *"Ready to connect"* to be displayed. This will take several seconds.
4. The *"Enable"* button within the ComputerSMS Android app should now be enabled, and the computer's IP address should be displayed below the button.
5. Select the *"Enable"* button within the ComputerSMS Android app.
6. The message *"Service started"* should now be displayed on both the desktop and Android applications.
7. To send a message from your computer:
  * Enter the 10 digit recipient's number in the *"Phone Number"* text box.
  * Enter the message in the *"Message"* text box.
  * Select the *"Send"* button.
8. Incoming text messages will be displayed in blue within the desktop application.
9. Incoming phone calls will be displayed in red within the desktop application.
10. Outgoing messages will be displayed in black within the desktop application.

#### Known Bugs:

* If the Android app is disabled while the ComputerSMSServer is running, both applications will need to be closed and restarted before the Android app can once again connect to the ComputerSMSServer.
* If the ComputerSMSServer is closed while the Android app is still enabled, the Android app will need to be disabled and restarted before it can once again connect to the ComputerSMSServer.

## Application Features

#### <u>Multi-Cast DNS with the JmDNS Library:</u>
[JmDNS](http://jmdns.sourceforge.net) is a Multi-Cast DNS implementation for Java used for service registration and discovery, allowing for automated service discovery. This feature was added to simplify the client/server connection. There is no need to manually find and enter the IP address, or hard code a port number within the desktop or Android applications.

#### <u>XML Message Passing:</u>

A standard XML format was used for message passing to simplify the creation of future servers or clients in languages other than Java. The standard XML message template is as follows:

{% highlight xml %}
<?xml version="1.0" encoding="utf-8" ?>
<smsMessage>
  <type></type>
  <number></number>
  <body></body>
</smsMessage>
{% endhighlight %}

The ComputerSMSServer desktop application uses [JaxB](https://jaxb.java.net) to map a SMSMessage object to the XML representation listed above.

The Android application uses [XMLSerializer](http://developer.android.com/reference/org/xmlpull/v1/XmlSerializer.html) to serialize an incoming SMS message or phone call into a valid XML message, and [XMLPullParser](http://developer.android.com/reference/org/xmlpull/v1/XmlPullParser.html) to parse an XML message received from the desktop application, creating a new SMSMessage object in the process.

#### <u>Encryption:</u>

Recognizing that these applications would likely be used in a public network setting, such as over open wifi at a coffee shop, encryption is a necessity. Exposure to man-in-the-middle attacks is a high risk so any intercepted messages must be completely secure. I used a combination of a Diffie-Hellman key exchange and AES to accomplish this encryption.

The chosen method of encryption was accomplished via the following:

* Diffie-Hellman Key Exchange - Once connected, a shared secret is generated from an agreed upon 1024 bit prime number, a base of two, and a secret key dynamically generated for each instance of each application. The result is a shared secret that is nearly impossible to crack.
* Advanced Encryption Standard (AES) - AES is a symetric-key algorithm that uses a shared private key for encryption and decryption. To alleviate the need for hardcoding this private key into each application, I used the shared secret generated from the Diffie-Hellman key exchange to compute the private key. The private key is calculated as the first 128 bits of the SHA-256 digest of the shared secret generated from the Diffie-Hellman key exchange. This results in a different private key each time the application is run.

## The ComputerSMSServer Java Desktop Application

<figure style="text-align: center">
    <img src="{{ site.url }}/images/android/computersms-desktop.png" alt="">
</figure>

The ComputerSMSServer desktop application broadcasts itself on the local network over UDP using Multi-Cast DNS, under the name ComputerSMS, and waits for a client to connect over TCP. Once connected to a client, the UDP broadcast is deregistered to ensure no other clients try to connect.

After a successful connection is made, a Diffie-Hellman key exchange is performed to calculate a shared secret between the server and client. The first 128 bits from the SHA-256 message digest of the shared secret is used for the private AES key. Once this key is calculated, the connection is encrypted and messages can be securely sent from the client to the server and vice versa.

#### <u>The ServerBoard Class:</u>

The ServerBoard class provides the basic swing based GUI. A JTextPane was used for the messages area to facilitate font format changes for the various message types. JTextFields were used for the *Phone Number* and *Message* fields, and JButtons were used for the *Start* and *Send* buttons.

The *Start* button instantiates a TCPServer with an anonymous TCPServer.OnMessageReceived object. The anonymous object overrides the messageReceived method, allowing it to unmarshall any incoming messages into SMSMessage objects and to display those incoming messages in the messages area.

The *Send* button constructs an SMSMessage object from the inputs in the *Phone Number* and *Message* fields, before marshalling this object into a valid XML message. Once the message is serialized into XML, it is sent to the client.

#### <u>The TCPServer Class:</u>

The TCPServer class extends the Thread class. When run, this class instantiates a ServerSocket with port 0 which assigns it the next available port. The service type and port are bundled into a JmDNS ServiceInfo object with the name *"ComputerSMS"* and the service is broadcast. The TCPServer then waits for a client to connect.

Once connected, the TCPServer sends out the Diffie-Hellman public key and waits to receive the clients public key. The shared secret is calculated and the AES private key is determined. Once the AES private key is set, the TCPServer sits in a loop waiting for incoming messages from the client that it decrypts and passes to the messageReceived method defined in the ServerBoard class.

#### <u>The SMSMessage Class:</u>

The simple SMSMessage class provides a framework for mapping XML messages to java objects via the JaxB libraries. Incoming XML messages are unmarshalled into an SMSMessage object, and outgoing messages are marshalled from a SMSMessage object into a valid XML message before transmission.

## The ComputerSMS Android Application

<figure style="text-align: center">
    <img src="{{ site.url }}/images/android/computersms-android.png" alt="">
</figure>

This application is composed of three components: the main activity, a broadcast receiver, and a service. The main activity allows the user to enable the service when the server application is detected on the local area network. Once enabled, the service starts a broadcast receiver that is invoked whenever a text message or incoming call is received, passing the received message to the service. The service then converts the message to XML and sends it to the server application. The service receives any incoming XML message from the server and sends it out as a SMS message.

#### <u>Required Permissions:</u>
* RECEIVE_SMS - Enables the application to read incoming SMS messages which it then passes to the desktop application.
* SEND_SMS - Allows the application to send SMS messages that it receives from the desktop application.
* INTERNET - Used to open a socket of communication between the Android application and the desktop application over a local area network.
* READ_PHONE_STATE - Allows the Android application to listen for incoming calls, notifying the desktop application each time an incoming call is received.
* ACCESS_WIFI_STATE - Enables access to the IP address of the device which is used in the discovery of services on the network.
* CHANGE_WIFI_MULTICAST_STATE - Enables the DNS Service Discovery functionality of JmDNS which is used to discover the appropriate service on the network.

#### <u>The MainActivity Class:</u>

The MainActivity class provides a simple GUI consisting of a single toggle button. When the application is opened, DNS Service Detection is enabled using the JmDNS library to look for a registered server on the network. Once found, the registered server's IP address and port number are extracted and the *"Enable"* toggle button is enabled.

When the user selects the *"Enable"* button, an Intent is created with the IP address and port number as extras. This intent is used to start the ComputerSMSService service class.

#### <u>The ComputerSMSService Class:</u>  

When the service is first created the onCreate method is called. This method instantiates and registers a ComputerSMSReceiver broadcast receiver with MESSAGE.SMS_RECEIVED and MESSAGE.CALL intent filters. Subsequent calls to the ComputerSMSService object will only call the onStart method, completely bypassing the onCreate method.

The onStart method handles four actions: start, incoming call, incoming sms message, and stop. The start action starts the foreground service that is accessible through the notifications bar and executes an AsyncTask that runs the TCPClient in the background. The incoming call and incoming SMS actions wrap the relevant call or SMS message information in XML before sending it to the server with the TCPClient. Finally, the stop action stops the TCPClient, foreground service, and ComputerSMSService.

#### <u>The ComputerSMSReceiver Class:</u>

The ComputerSMSReceiver is notified of any incoming SMS messages or phone calls. The receiver then builds an Intent with the relevant information (action type, number, message, etc.), and starts the ComputerSMSService with that intent.

#### <u>The TCPClient Class:</u>

The TCPClient class listens for incoming messages from the server and sends outgoing messages to the server. When the run method is called, a Socket to the server is instantiated and a PrintWriter stream is opened for output. The Diffie-Hellman public key is sent to the server over this output stream. A BufferedReader input stream is then opened, and the client waits for the server to send its Diffie-Hellman public key. The client uses the received public key to calculate the Diffie-Hellman shared secret and AES private key, thereby establishing encryption of the connection. Once the connection is encrypted, the TCPClient sits in a loop waiting for incoming messages and sending outgoing messages.

#### <u>The SMSMessage Class:</u>

The SMSMessage class provides a framework for mapping incoming XML messages to java objects using the XMLPullParser. Incoming XML messages are parsed, creating a SMSMessage object in the process.

## Conclusion

Not only did this project produce a useful set of applications that solved a personal problem, but it also expanded and solidified my knowledge in several important computing topics. These topics include:

* Threading - DNS service discovery and messaging clients run in threads separate from the main thread.
* Multi-Cast DNS - Using Multi-Cast DNS and DNS-SD through the JmDNS library allowed for a greatly simplified network connection process. With this method, there is no need to manually determine IP addresses or to hard code port numbers.
* Diffie-Hellman Key Exchange - Using the Diffie-Hellman key exchange allowed for a dynamically generated AES private key.
* AES Encryption - The use of a hard coded AES encryption private key was avoided by using the Diffie-Hellman key exchange to dynamically generate private keys.
* XML Messaging - XML was used to generate standard message layouts to simplify the development of future clients in languages other than Java. JaxB was used to simplify XML parsing within the desktop application, and the combination of the XMLSerializer and XMLPullParser were used within the Android application.

Overall, this was a phenomenal learning experience that resulted in a personally useful final product.
