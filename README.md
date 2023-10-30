# t440p-bios-mod

## Dump current bios image
```shell
sudo flashrom -p ch341a_spi -r 2.56.img
sudo flashrom -p ch341a_spi -r 2.56_double_check.img
diff 2.56.img 2.56_double_check.img
```

## Path bios image
### Method 1 - remove wifi whitelist and activate advanced menu
```shell
./UEFIPatch 2.56.img xx40_xx50_patches_v7.txt -o 2.56_full.img
./thinkpad-uefi-sign/sign.py 2.56_full.img -o 2.56_full.img
./thinkpad-uefi-sign/verify.py 2.56_full.img
```

### Method 2 - remove wifi whitelist only
./UEFIPatch 2.56.img xx40_xx50_patches_v7_only_wifi.txt -o 2.56_wifi.img
./thinkpad-uefi-sign/sign.py 2.56_wifi.img -o 2.56_wifi.img
./thinkpad-uefi-sign/verify.py 2.56_wifi.img

## Write patched bios image
sudo flashrom -p ch341a_spi -w 2.56_full.img
