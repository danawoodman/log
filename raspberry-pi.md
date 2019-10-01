# Raspberry Pi Resources

### Headless RPI install

From [this article](https://desertbot.io/blog/headless-pi-zero-w-wifi-setup-windows)

1. Download [Raspbian Lite image from here](https://www.raspberrypi.org/downloads/raspbian/)
2. Use [Balena Etcher](https://www.balena.io/etcher/) to flash your SD with Raspbian Lite
3. Mount the SD card after flashing
4. Create a file called `ssh` in the root of the SD card to enable SSH
5. Create a file called `wpa_supplicant.conf` in the root of the SD card to configure WiFi:

```
country=US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
   ssid="NETWORK-NAME"
   psk="NETWORK-PASSWORD"
}
```

6. Put SD card in RPi and turn it on
7. SSH to the RPi with: `ssh pi@raspberrypi.local`
8. Optional: change your hostname with `sudo raspi-config`


### Setup a RPI as a Bluetooth audio server

From [this guide](https://circuitdigest.com/microcontroller-projects/diy-raspberry-pi-bluetooth-speaker) and [this one](https://scribles.net/streaming-bluetooth-audio-from-phone-to-raspberry-pi-using-alsa/):

1. Setup dependencies:

```
sudo apt install bluez pulseaudio-*.
```

2. Setup Bluetooth to be discoverable:

```
$ sudo bluetoothctl
# agent on
# default-agent
# discoverable on
```

3. Now connect to the RPi with your phone.
4. In `bluetoothctl` you will see the phone connect, copy the MAC address into:

```
trust <MAC_ADDRESS>
connect <MAC_ADDRESS>
```

5. 

