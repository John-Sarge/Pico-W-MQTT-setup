# Pico-W-MQTT-setup

This script for the Raspberry Pi Pico W using MicroPython integrates with MQTT (Message Queuing Telemetry Transport), a lightweight messaging protocol for small sensors and mobile devices, to publish and subscribe to messages over the network. It demonstrates a basic IoT (Internet of Things) application where the Pico W acts as both a publisher of messages and a subscriber to commands that control an onboard LED.

### Detailed Explanation

1.  Imports and Setup

    -   The script imports necessary modules for time tracking, generating unique IDs, MQTT communication, controlling hardware pins, and generating random numbers.
    -   `MQTT_BROKER` is the IP address or hostname of the MQTT broker to which the Pico W connects.
    -   `CLIENT_ID` is a unique identifier for the MQTT client, generated from the Pico W's unique hardware ID.
    -   `SUBSCRIBE_TOPIC` and `PUBLISH_TOPIC` are MQTT topics for subscription and publishing, respectively.
2.  LED Setup

    -   The onboard LED of the Pico W is set up as an output device. Commands received from the MQTT broker on the `SUBSCRIBE_TOPIC` will control this LED.
3.  MQTT Message Handling

    -   `sub_cb` is a callback function that handles messages received on the subscribed topic. If a message "ON" is received, the LED turns on; otherwise, it turns off.
4.  MQTT Connection and Communication

    -   The script creates an instance of `MQTTClient` with the specified broker address and client ID. It sets the callback function for handling messages and connects to the broker.
    -   It subscribes to the `SUBSCRIBE_TOPIC`, ready to receive and act upon messages.
5.  Publishing Messages

    -   Inside the main loop, the script continuously checks for incoming messages without blocking (`mqttClient.check_msg()`).
    -   It publishes messages at a defined interval (`publish_interval`). The published messages are dummy data strings with timestamps, meant to represent sensor data like temperature readings. Note: The `publish_interval` is set to `0.001`, which is very short and might not be practical for real applications. This could lead to rapid message publishing, potentially overwhelming the broker or consuming excessive bandwidth.
6.  Error Handling and Resets

    -   The main function is wrapped in a try-except block to catch `OSError` exceptions, which may occur during network communication failures. Upon catching an error, the script attempts a soft reset after a delay.
7.  Infinite Loop

    -   The script runs in an infinite loop, attempting to reconnect and resume operation after errors.

### Key Considerations

-   MQTT Broker: Requires an MQTT broker (like Mosquitto, HiveMQ, etc.) running and accessible by the IP address specified in `MQTT_BROKER`.
-   Network Configuration: The Pico W's connection to the network is assumed to be configured separately in the `boot.py` file, which runs before this script and sets up WiFi connectivity.
-   Topic Subscription and Publishing: The script illustrates basic IoT communication patterns---listening for commands to control local hardware and publishing data to the network.
-   Error Handling: The script attempts to handle disconnections or network errors gracefully by resetting the Pico W.

This script is a foundation for more complex IoT applications, where devices interact with each other and with servers over the internet using MQTT for messaging.

created by [John Seargeant](https://github.com/John-Sarge) with a little help from GPT and Bard.  03Feb2024
