# huawei-r4850g2-esphome
ESPHome project for huawei r4850g2 rectifier with can bus control.

This project is inspired by 
  - https://github.com/craigpeacock/Huawei_R4850G2_CAN/
  - https://github.com/KlausLi/Esp-HuaweiR4850-Controller

The first is in C and meant to run based on linux on a raspberry pi or similar.

The second is more specialized for a charge control in combination with solar power. And more important: is it close source and has a bit strange api.

That why I tried to do this with pure ESPHome and do all the automation part in home assistant.

# Wiring

Wiring is exactly the same as in https://github.com/KlausLi/Esp-HuaweiR4850-Controller please lookup the wiring in this project.

# Home assistant

I prefer to route everything via mqtt, so this project doesn't need to share an API key with home assistant. Instead add the address of your mqtt server to your secrets.yaml file.
![Secrets](/images/secrets.png)

