# WiFi can bus controller for huawei r4850g2 or r4850g1 with ESPhome
ESPHome project for huawei r4850g2 or r4850g1 rectifier with can bus control.

It uses a cheap D1 mini module (ESP8266) and a can bus module MCP2515. Alternatively you can also use a ESP32 and a can bus transceiver.
There are lots of boards and modules available just search for "esp32 canbus".

This project is inspired by 
  - https://github.com/craigpeacock/Huawei_R4850G2_CAN/
  - https://github.com/KlausLi/Esp-HuaweiR4850-Controller
  - https://github.com/mb-software/esphome-huawei-r4850

The first is in C and meant to run on linux on a raspberry pi or similar. Also I noticed that the factors for current are wrong.

The second is more specialized for a charge control in combination with solar power. And more important: is it closed source and has a strange api.

The 3rd is a mix of ESPHome with custom components in python and c++ and seems unneccesary complex. But in this implementation the factors for current seem to be correct.

That's why I tried to do this with pure ESPHome and do all the automation part in home assistant.

# Wiring

Wiring is exactly the same as in https://github.com/KlausLi/Esp-HuaweiR4850-Controller please lookup the wiring in this project.

Basically this is the setup:
![wiring](/images/wiring.png)

The "BavarianSuperGay" adds another special trick: while the MCP2515 is running with 3v3 to keep it compatible to the ESP, the can bus transceiver is feed with 5v. Not sure if this is really necessary, but it works fine. To do this you need to modify the can bus module see https://youtu.be/2mAzP_35Ox8

# Additional settings

## online / offline
In addition to the settings supported on the can bus there is a **online/offline** switch, that allows to also test the offline mode without disconnecting the can bus. When set to "offline" the controller stop sending data requests which make the huawei r4850 "go offline" after around 30 seconds. You will notice the yellow led at the front blinking and output voltage and current are change to the offline default.

When giong back online the controller will automatically restore the latest "online" values for voltage and current.

## max_current placeholder

You can set the max current of your rectifier at the beginning of the yaml file so it works for 50A type and for 75A types as well.

# Home assistant

I prefer to route everything via mqtt, so this project doesn't need to share an API key with home assistant. Instead add the address of your mqtt server to your secrets.yaml file.
![Secrets](/images/secrets.png)

The home assistant auto discovery via mqtt creates immediate cards for your dashboards
![ha](/images/ha.png)