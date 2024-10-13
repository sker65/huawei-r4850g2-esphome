# huawei-r4850g2-esphome
ESPHome project for huawei r4850g2 rectifier with can bus control.

It uses a cheap D1 mini module (ESP8266) and a can bus module MCP2515. Alternatively you can also use a ESP32 and a can bus transceiver.
There are lots of boards and modules available just search for "esp32 canbus".

This project is inspired by 
  - https://github.com/craigpeacock/Huawei_R4850G2_CAN/
  - https://github.com/KlausLi/Esp-HuaweiR4850-Controller

The first is in C and meant to run based on linux on a raspberry pi or similar.

The second is more specialized for a charge control in combination with solar power. And more important: is it closed source and has a strange api.

That's why I tried to do this with pure ESPHome and do all the automation part in home assistant.

# Wiring

Wiring is exactly the same as in https://github.com/KlausLi/Esp-HuaweiR4850-Controller please lookup the wiring in this project.

Basically this is the setup:
![wiring](/images/wiring.png)

The "BavarianSuperGay" adds another special trick: while the MCP2515 is running with 3v3 to keep it compatible to the ESP, the can bus transceiver is feed with 5v. Not sure if this is really necessary, but it works fine. To do this you need to modify the can bus module see https://youtu.be/2mAzP_35Ox8

# Home assistant

I prefer to route everything via mqtt, so this project doesn't need to share an API key with home assistant. Instead add the address of your mqtt server to your secrets.yaml file.
![Secrets](/images/secrets.png)

