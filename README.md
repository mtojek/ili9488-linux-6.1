# ili9488-linux-6.1

## Pinout

Limitation: Do not link screen's MISO and touch's DOUT lines together, as XPT2046 can't support it (X = 0, Y = 0). Unfortunately, you need to use separate SPI buses.

## DTS

```bash
dtc -@ -I dts -O dtb -o 3.5_ips_spi_320x480.dtbo 3.5_ips_spi_320x480.dts
sudo mv 3.5_ips_spi_320x480.dtbo /boot/overlay-user/
```

Add `user_overlays=sun50i-h616-3.5_ips_spi_320x480` to `/boot/orangepiEnv.txt`.

## Setup panel-mipi-dbi

More details: https://github.com/notro/panel-mipi-dbi/wiki

```bash
python3 mipi-dbi-cmd.py panel-mipi-dbi-spi.bin panel-mipi-dbi-spi.txt
sudo cp panel-mipi-dbi-spi.bin /lib/firmware/
sudo update-initramfs -u
```
