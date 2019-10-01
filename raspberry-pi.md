# Raspberry Pi Resources

## Headless RPI install

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


## Setup a RPI as a Bluetooth audio server

Just use [this guide to get things setup using balena](https://www.balena.io/blog/turn-your-old-speakers-or-hi-fi-into-bluetooth-receivers-using-only-a-raspberry-pi/).



#### Older versions....



```shell
$ sudo apt update -y
$ sudo apt upgrade -y
$ sudo apt install -y bluealsa bluez bluetooth pulseaudio-module-bluetooth
$ pulseaudio --start
$ sudo pactl unload-module module-bluetooth-discover
$ sudo pactl load-module module-bluetooth-discover
$ sudo bluetoothctl
# agent on
# default-agent
# discoverable on
# scan on
# trust <MAC_ADDRESS>
# pair <MAC_ADDRESS>
# conect <MAC_ADDRESS>
# exit
$ sudo /bin/hciconfig hci0 inqdata "0c097261737062657272797069020a00091002006b1d460217050d03001801180e110c1115110b1100"
$ sudo bluealsa -p a2dp-sink &
$ sudo bluealsa-aplay F0:C3:71:1F:3E:71 &
```

- [ ] Set this all up with a simple script
- [ ] Run this as a system service

From [this guide](https://circuitdigest.com/microcontroller-projects/diy-raspberry-pi-bluetooth-speaker) and [this one](https://scribles.net/streaming-bluetooth-audio-from-phone-to-raspberry-pi-using-alsa/):

1. Setup dependencies:

```shell
sudo apt update -y
sudo apt upgrade -y
sudo apt install -y bluealsa bluez pulseaudio-*.
sudo bluealsa -p a2dp-sink &
```

2. Setup Bluetooth to be discoverable:

```shell
$ sudo bluetoothctl
# agent on
# default-agent
# discoverable on
```

3. Now connect to the RPi with your phone.
4. In `bluetoothctl` you will see the phone connect, copy the MAC address into:

```shell
trust <MAC_ADDRESS>
connect <MAC_ADDRESS>
pair <MAC_ADDRESS>
```

5. Run the following (no idea why this works or is needed...)

```shell
sudo hciconfig hci0 leadv 0
sudo hciconfig hci0 leadv 3
sudo /bin/hciconfig hci0 inqdata "0c097261737062657272797069020a00091002006b1d460217050d03001801180e110c1115110b1100"
```

   Note: you can change the name of your Bluetooth device by following [this Stack Overflow answer](https://stackoverflow.com/a/49988428/529829).
6. Start pulseaudio daemon:

```shell
pulseaudio --start

# make sure it worked:
pactl list short
```

7. Run bluealsa:

```shell
sudo bluealsa -p a2dp-sink &
sudo bluealsa-aplay <MAC_ADDRESS> &
```

### Start pulseaudio on boot:

[Start pulseaudio on boot](https://rudd-o.com/linux-and-free-software/how-to-make-pulseaudio-run-once-at-boot-for-all-your-users):

```shell
sudo vi /etc/systemd/system/pulseaudio.service
```

Then paste in:

```ini
[Unit]
Description=PulseAudio system server

[Service]
Type=notify
ExecStart=pulseaudio --daemonize=no --system --realtime --log-target=journal

[Install]
WantedBy=multi-user.target
```

Then run:

```shell
sudo systemctl enable pulseaudio.service
sudo systemctl start pulseaudio.service
```

#### Other resources/tips:

- Adjust audio level on RPi via command line: `sudo alsamixer`
