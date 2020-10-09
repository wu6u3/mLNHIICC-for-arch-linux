# mLNHIICC-for-arch-linux
Taiwan National Health Insurance Card (台灣健保卡網路服務) Smart Card Reader on Arch Linux x86_64

This is the scripts for installing the National Health Insurance Card for the online service. 

台灣健保卡網路服務讀卡機元件只提供 Ubuntu 以及 Fedora 這兩個Linux disribution

[NHI online service](https://cloudicweb.nhi.gov.tw/cloudic/system/mlogin.aspx)

這裡提供一個在Arch Linux 上面安裝元件的修正

## Prerequest 

1. Prepare a smart card reader that is compatible with Linux. 

``` 
pacman -S pcsc-tools pcsclite pcsc-perl libccid ccid 
```

2. Enable & start pcscd service

```
sudo systemctl start pcscd
sudo systemctl enable pcscd
```

3. Test card reader

```
pcsc_scan
```

Should get something like 

```
Using reader plug'n play mechanism
Scanning present readers...
0: <Your card reader> 00 00
 
Fri Oct ... <Time>
 Reader 0: <Your card reader>  00 00
  Event number: 3
  Card state: Card removed, 
```

Reference:
[1]. [ARCHLINUX下用WEBATM轉帳](https://dd-han.tw/2016/archlinux-webatm)
[2]. [ArchLinux 晶片讀卡機的安裝](https://w2b2.blogspot.com/2012/06/archlinux.html)


## Install mLNHIICC 安裝健保卡讀卡機元件

1. 去[健保卡網路註冊](https://cloudicweb.nhi.gov.tw/cloudic/system/mlogin.aspx)的網站 

2. 點選"首次登入請先申請 Register for New Account" -> 閱讀完畢並且了解相關規定 

3. 滑到頁面下半部點選 作業系統：Linux(Ubuntu)　[下載元件安裝檔](https://cloudicweb.nhi.gov.tw/cloudic/system/SMC/mLNHIICC_Setup.Ubuntu.zip)


4. 解壓縮 mLNHIICC_Setup.Ubuntu.zip -> 再次解壓縮 mLNHIICC_Setup.tar.gz

5. Replace the script for install
``` 
cd mLNHIICC_Setup
mv <path_to_this_git_repo>/Install_arch_linux_64.sh Install
sudo chmod 755 Install
./Install
``` 

6. 點網頁上 "步驟2:設定伺服器為可信任服務"
並且
```
sudo /usr/local/share/NHIICC/mLNHIICC &
```
7. 點選網上 檢測健保卡認證 就可以順利讀卡(記得插入健保卡)以及連線

Testing Env:
Arch Linux x86_64 (Sep-26-2020)
Chrome 85.0.4183.121






















