# ILI9488 | linux-6.1 | LiangHaoCai LHC3540-IPS

Tested on: OrangePi Zero 2W, kernel 6.1.31 

<img src="https://github.com/mtojek/ili9488-linux-6.1/raw/main/misc/photos/3.jpeg" width="300"/>

## Pinout

Limitation: Do not link screen's MISO and touch's DOUT lines together, as XPT2046 can't support it (X = 0, Y = 0). Unfortunately, you need to use separate SPI buses.

## Driver

Based on OrangePi Zero 2W driver, Kernel version: `6.1.31-sun50iw9 #1.0.4`

```bash
git clone https://github.com/orangepi-xunlong/linux-orangepi/
./build.sh docker
```

Then, copy over driver files from this repo, and:

```
./build.sh docker
```

Kernel deps will be in `output/debs`:

```bash
$ ls -l output/debs/
total 48612
drwxrwsr-x 2 root docker     4096 Aug  3 08:18 extra
-rw-r--r-- 1 root docker    15092 Aug  6 19:07 linux-dtb-next-sun50iw9_1.0.4_arm64.deb
-rw-r--r-- 1 root docker 12461512 Aug  6 19:07 linux-headers-next-sun50iw9_1.0.4_arm64.deb
-rw-r--r-- 1 root docker 36035344 Aug  6 19:07 linux-image-next-sun50iw9_1.0.4_arm64.deb
-rw-r--r-- 1 root docker  1250676 Aug  6 19:07 linux-libc-dev_1.0.4_arm64.deb
drwxrwsr-x 2 root docker     4096 Aug  3 08:18 u-boot
```

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

## Photos

<p float="left">
  <img src="https://github.com/mtojek/ili9488-linux-6.1/raw/main/misc/photos/1.jpeg" width="300"/>
  <img src="https://github.com/mtojek/ili9488-linux-6.1/raw/main/misc/photos/2.jpeg" width="300"/>
  <img src="https://github.com/mtojek/ili9488-linux-6.1/raw/main/misc/photos/3.jpeg" width="300"/>
  <img src="https://github.com/mtojek/ili9488-linux-6.1/raw/main/misc/photos/4.jpeg" width="300"/>
  <img src="https://github.com/mtojek/ili9488-linux-6.1/raw/main/misc/photos/5.jpeg" width="300"/>
</p>
