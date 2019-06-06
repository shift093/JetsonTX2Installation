### 安裝指南

#### 準備

兩台PC
一台TX2

一台自動DHCP分享器
兩條網路線(TX2、主機需要同一個網域底下)


#### 步驟一
下載jetpack到主機(ubuntu16.04)
https://developer.nvidia.com/embedded/downloads

sudo apt update
sudo apt grade

#### 步驟二

先在主機安裝sdk manager
cd Dowloads
ls ./sdk...(tab)
```
sudo apt install ./skdmanager...(tab)
```
run
```
skdmanager
```

#### 步驟三

選擇 host+tx2
打勾
等待安裝 flash(~ Insatalling... 50%)

主機這邊:用其他電腦VNC遠端控制主機
螢幕接TX2(這時候已經安裝好TX2的OS了，會有畫面)
設定帳號密碼等等...結束後
登入TX2`ifconfig`查TX2虛擬IP(待會要在主機那邊登入TX2，以便安裝SDK檔案)

取得ip後到主機這邊輸入ip及帳密，開始安裝SDK

主機有安裝opencv會衝突，導致TX2安裝過程computer vision會Error
