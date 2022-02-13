# raspbee2-deconz

I have a [Phoscon Raspbee II](https://phoscon.de/en/raspbee2), attached to a Raspberry Pi Zero 2W.

The `deconz` application is deployed via the [community docker image](https://github.com/deconz-community/deconz-docker).


### Setup

To run on Raspbian under docker,
[some changes need to be made](https://github.com/deconz-community/deconz-docker#configuring-raspbian-for-raspbee)
to the serial device, making the Raspbee appear on `/dev/ttyAMA0`.

```
echo 'dtoverlay=pi3-miniuart-bt' | sudo tee -a /boot/config.txt
```

### Operation

This docker image _must_ expose 80 and 443 in order for pairing and comms to be successful.

The control panel web UI can be found at:

http://caul:8080/pwa/login.html


### Raspbee firmware upgrade

Following the [upgrade instructions](https://github.com/deconz-community/deconz-docker#updating-conbeeraspbee-firmware),
one can check for new firmwares here:

* http://deconz.dresden-elektronik.de/deconz-firmware

At time of writing firmware was updated to `0x26720700`.

Stop the `deconz` docker container and run the following upgrade script:

```
docker run -it --rm --entrypoint /firmware-update.sh \
  --privileged --cap-add=ALL \
  -v /dev:/dev -v /lib/modules:/lib/modules -v /sys:/sys \
  marthoc/deconz
```


## IKEA Tradfri

I have a few TRADFRI 30w Driver devices as smart switches for attached LED lighting.

* Make sure that a light is attached during reset/pairing
* Reset only takes a couple of seconds; watch for the lights to flash and come back on
* Flicking the lights off-on once during pairing (as advised) was helpful



