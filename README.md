# t440p-bios-mod

## 1. Dump current bios image
```shell
sudo flashrom -p ch341a_spi -r 2.56.img
sudo flashrom -p ch341a_spi -r 2.56_double_check.img
diff 2.56.img 2.56_double_check.img
```

## 2. Path bios image
### Method 1 - remove wifi whitelist and activate advanced menu
```shell
./UEFIPatch 2.56.img xx40_xx50_patches_v7.txt -o 2.56_full.img
./thinkpad-uefi-sign/sign.py 2.56_full.img -o 2.56_full.img
./thinkpad-uefi-sign/verify.py 2.56_full.img
```

### Method 2 - remove wifi whitelist only
```bash
./UEFIPatch 2.56.img xx40_xx50_patches_v7_only_wifi.txt -o 2.56_wifi.img
./thinkpad-uefi-sign/sign.py 2.56_wifi.img -o 2.56_wifi.img
./thinkpad-uefi-sign/verify.py 2.56_wifi.img
```

## 3. Write patched bios image
```bash
sudo flashrom -p ch341a_spi -w 2.56_full.img
```
