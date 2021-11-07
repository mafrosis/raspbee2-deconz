# raspbee2-deconz

I have a [Phoscon Raspbee II](https://phoscon.de/en/raspbee2), attached to a Raspberry Pi 3B.

Using the [docker method](https://phoscon.de/en/raspbee2/install#docker)


### Setup

To run on Raspbian under docker,
[some changes need to be made](https://github.com/marthoc/docker-deconz#configuring-raspbian-for-raspbee)
to the serial devices to allow the Raspbee to appear on `/dev/ttyAMA0`.

```
echo 'dtoverlay=pi3-miniuart-bt' | sudo tee -a /boot/config.txt
```

http://kvothe:8080/pwa/login.html


### Raspbee firmware upgrade

Following the [upgrade instructions](https://github.com/marthoc/docker-deconz#updating-conbeeraspbee-firmware),
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

I have a few TRADFRI 30w Driver devices as smart switches for attached LED lighting. They can a bit
of a pain to pair, but it worked eventually

