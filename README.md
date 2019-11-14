# esphome-energy6channel
[ESPHome](https://esphome.io) configuration and steps used to created energy montiroing boards using an ESP32 chip with a energy board capable of reading 6 CT Clamps across 6 circuits.  Integration completed to [Home Assistant](https://home-assistant.io) using API from esphome.  

# Overview
ESPHome device was built using a video from [digiblurDIY](https://www.youtube.com/watch?v=BOgy6QbfeZk) tutorial for guidance.  

My process was modified as I run Home Assistant in a container and do not run Hass.io, therefore I ran esphome in a docker container using the script in my repo.  I also had to tune / calibrate the Volts gain and amp gain to get correct calibration for my home.  Be sure to perform USB flash initially as noted with the ESP32 chip not connected to the board.


## Parts List
- Split Core Current Transformers 100A/50ma (Note these were too small to fit around my main feeds.  Recommend measuring or using the larger split core if planning to use on your main power feeds. [Link](https://www.amazon.com/MIKIKI-SCT-013-000-Non-invasive-Current-Transformer/dp/B07C6TDDWM/ref=as_li_ss_tl)
- ESP32-S NodeMCU [Link](https://www.amazon.com/HiLetgo-ESP-WROOM-32-Development-Microcontroller-Integrated/dp/B0718T232Z/ref=as_li_ss_tl)
- 9VAC Power Supply(THIS IS AC NOT DC) - [Link](https://www.amazon.com/gp/product/B00B886CWS/ref=as_li_ss_tl)
- CircuitSetup 6 Channel Board - [Link](https://circuitsetup.us/index.php/product/expandable-6-channel-esp32-energy-meter/)
## Config YAML
- [energy_6c_1](https://github.com/mcaminiti/esphome-energy6channel/blob/master/energy_6c_1/energy_6c_1.yaml)

## Docker Information
Docker - esphome/esphome:dev
```docker run -d -v "/LOCAL/PATH/esphome/config:/config" --net=host esphome/esphome:dev```

## Software
- [ESPHome Flasher](https://github.com/esphome/esphome-flasher/releases) - Used to flash initial config to ESP32.  Used this utility on a Mac and it required extra drivers installed for serial to USB. 
- [Drivers](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers) - Installed these drivers to make the Serial port show up when connecting as USB to Mac.

## Calibration
I used a clamp meter on a custom built cord to allow me to place the CT clamp and the clamp meter on the same device.  I used a 55 W Rough Service Incadescent bulb to tune the Volts by adjusting gain_voltage until it matched my house voltage.  Then changed the gain for the amp readings to match the draw.  I used the web page from the ESP device to view readings of amp/watts while tuning.  Each clamp was calibrated but all in my set were the exact same settings. 

## Project Pictures
![UI](images/esphome-1.jpeg?raw=true "Parts")
![UI](images/esphome-2.jpeg?raw=true "Programmed")
![UI](images/esphome-3.jpeg?raw=true "Installed")
![UI](images/ha-1.png?raw=true "Home-Assistant")
