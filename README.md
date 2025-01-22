## Steam Link on Raspberry Pi with autostart

Setting up steam link on my raspi. Tested in January 2025 on my raspberry model 4 with Raspbian 64 bit (Bookworm).

## Setup

1. Install Raspbian with Raspberry Pi Imager

2. Update & Install Steamlink

Installing steamlink is fairly straightforward.

```
apt upgrade -y && apt update -y
apt install steamlink
```

That's it. You can start it with `steamlink` from console. There should also be a handy shortcut on your desktop.

3. Autostarting steamlink on boot

This one was a bit frustrating and tricky. Because I want to use my raspi like a gaming console on my living room TV, this part was pretty crucial. Having a keyboard connected to my pi and starting steamlink manually isn't the ideal experience for this setup.

Unfortunately, most solutions I found online were outdated and didn't work for me.

What finally worked for me was editing `~/.config/labwc/autostart` to contain the following:

```
sleep 10
/usr/bin/steamlink &
```

The `sleep` command was a necessary workaround to stop steamlink from starting too early. This would cause steamlink to check for updates before the network was ready, thereby causing an error.


## Troubleshooting

### Sound Issues over HDMI

Initially, I had no sound with my HDMI cable. What fixed it for me was calling:

```
raspi-config
```

Here in `System Options > Audio >` make sure HDMI output is selected.

For some people, it seems to be necessary to edit `/boot/firmware/config.txt` (previously located at /boot/config.txt) to fix this issue. See https://raspberrypi.stackexchange.com/questions/32717/how-to-enable-sound-on-hdmi.


### Slow Wi-Fi Internet Speed when using HDMI

Unfortunately, I didn't find a good solution to this issue. Instead, I switched to an Ethernet cable.

Apparently, this problem can be reduced (but not solved) by connecting your HDMI cable to HDMI0 instead of HDMI1. HDMI0 is the one closer to the power connector.
