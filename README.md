# TFT43-DIP Drivers
TFT43-DIP is an display for the Raspberry Pi with capacitive touchscreen.

# Note
* The Raspberry Pi OS after `2022-04-04` has a built-in DPI driver, so we only need a simple configuration in `/boot/config.txt` file to use this screen.
* The OS of `2022-09-22` displays that the 180 degree rotation function is abnormal, please do not use it.

## Display function
Add the following configuration to the `[all]` section of the `/boot/config.txt` file. (Generally, it can be added to the bottom of the `/boot/config.txt` file)
```
dtoverlay=vc4-kms-dpi-generic
dtparam=rgb666-padhi,clock-frequency=32000000
dtparam=hactive=800,hfp=16,hsync=1,hbp=46
dtparam=vactive=480,vfp=7,vsync=3,vbp=23
dtparam=backlight-gpio=19
dtparam=rotate=0
```
`rotate` = Display rotation, The values that can be set include `0`, `90`, `180`, `270`. The default value is `0`

## Touch function
Copy [`gt911_btt_tft43_dip.dtbo`](./gt911_btt_tft43_dip.dtbo) file to `/boot/overlays` path. (We can copy the file to the boot path of the SD card on the computer, or execute the following command on the ssh of the Raspberry Pi to download it directly)
```
sudo wget https://raw.githubusercontent.com/bigtreetech/TFT43-DIP/master/gt911_btt_tft43_dip.dtbo -O /boot/overlays/gt911_btt_tft43_dip.dtbo
```
And add the following configuration to the `[all]` section of the `/boot/config.txt` file.
```
dtoverlay=gt911_btt_tft43_dip
dtparam=rotate_0
```
`rotate_*`= Touch rotation, This `dtparam` can be set to `rotate_0`, `rotate_90`, `rotate_180`, `rotate_270`. Corresponding to display rotation.

## For example

### Normal display
* Copy [`gt911_btt_tft43_dip.dtbo`](./gt911_btt_tft43_dip.dtbo) file
* Add the following configuration to the `[all]` section of the `/boot/config.txt` file
  ```
  dtoverlay=vc4-kms-dpi-generic
  dtparam=rgb666-padhi,clock-frequency=32000000
  dtparam=hactive=800,hfp=16,hsync=1,hbp=46
  dtparam=vactive=480,vfp=7,vsync=3,vbp=23
  dtparam=backlight-gpio=19
  dtparam=rotate=0

  dtoverlay=gt911_btt_tft43_dip
  dtparam=rotate=0
  ```

### Rotate 90 degrees display
* Copy [`gt911_btt_tft43_dip.dtbo`](./gt911_btt_tft43_dip.dtbo) file
* Add the following configuration to the `[all]` section of the `/boot/config.txt` file
  ```
  dtoverlay=vc4-kms-dpi-generic
  dtparam=rgb666-padhi,clock-frequency=32000000
  dtparam=hactive=800,hfp=16,hsync=1,hbp=46
  dtparam=vactive=480,vfp=7,vsync=3,vbp=23
  dtparam=backlight-gpio=19
  dtparam=rotate=90

  dtoverlay=gt911_btt_tft43_dip
  dtparam=rotate=90
  ```
