# 安裝指南

新增版本
https://www.jetsonhacks.com/2019/07/22/jetpack-4-2-1-release/

# 準備

```
* 兩台PC(ubuntu16.04+window8.1)
* 一台TX2
* 一台螢幕支援hdmi
* 一台自動DHCP分享器
* 至少一條網路線(TX2、主機需要同一個網域底下,無線就只需要一條把TX2跟主機串起來)
```

# 步驟一


[https://developer.nvidia.com/embedded/downloads](https://developer.nvidia.com/embedded/downloads)
```
# 下載jetpack到主機(ubuntu16.04)
sudo apt update
sudo apt upgrade
```

# 步驟二

```
# 先在主機安裝sdk manager
cd Dowloads
ls ./sdk...(tab)
sudo apt install ./skdmanager...(tab)
# run sdk manger
skdmanager
```

# 步驟三

```
登入後

a. 選擇 tx2就好 主機(HOST)不用

b. 打勾,同意

c. 等待安裝,flash(~ Insatalling... 50%)

  c1. 過程如果跳出視窗需要(manual)手動重置tx2
  
  c2. 長按power強制關機tx2,拔電源線,重新接上開機,按recovery兩秒接著按reset放開後,等兩秒再放開recovery
  
  c3. `lsusb`查看是否usb有抓到`Nvidia Cropertion`==tx2板子
  
d. 主機:用其他電腦VNC遠端控制主機(只有一個螢幕的方法)

# 螢幕接TX2(這時候已經安裝好TX2的OS了，會有畫面)

# tx2:設定帳號密碼等等...

# 登入後一樣打開terminal,先更新(順便確認連到網路且正常)

sudo apt update
sudo apt upgrade

#更新完

# 主機這邊輸入及帳密，開始安裝SDK(這個過程可以不用連到網路)
OS
TensorRT
cuDNN
VisionWorks
CUDA 10.0
Multimedia API
OpenCV...

安裝完就可以直接操作tx2
```

###### 註記:一般建議


# 步驟四

creating-a-swap-file
      
      $ df -h 
      這將顯示您的文件系統以及剩餘的空間。
      
      $ sudo fallocate -l 8.0G /swapfile 
      創建一個8 GB的交換
      
      $ sudo chmod 600 /swapfile 
      更改文件權限
      
      $ sudo mkswap /swapfile 
      
      $ sudo swapon /swapfile 
      
      $ free -m
      這將顯示交換文件已打開。您也可以拔出系統監視器
      但是這只是暫時的。如果重新啟動，交換文件就會消失。 
      
      $ sudo nano /etc/fstab 
      
      在此文件中添加“/swapfile none swap 0 0”行。不要包括引號。
      退出並保存文件
      
      現在您可以重新啟動並激活您的交換。 
# 步驟五

在TX2設定VNC 的 server, nvidia官方用`vino`
      
# 安裝常用套件
`sudo apt install ssh vino`

# 設定VNC 桌面遠端(desktop sharing) -> 
  * 預設為disable所以需要再設定
      ```
      export DISPLAY=:0
      gsettings set org.gnome.Vino enabled true
      gsettings set org.gnome.Vino prompt-enabled false
      gsettings set org.gnome.Vino require-encryption false
      /usr/lib/vino/vino-server
      
      # 沒辦法work?錯誤？
      ps aux | grep X
      DISPLAY=:1 /usr/lib/vino/vino-server
      
      # 錯誤？ Vino' does not contain a key named 'enable'?
      sudo vi /usr/share/glib-2.0/schemas/org.gnome.Vino.gschema.xml
      
      # 編輯 
      sudo nano /usr/share/glib-2.0/schemas/org.gnome.Vino.gschema.xml
      
      # 在key那層插入
      <key name='enabled' type='b'>
         <summary>Enable remote access to the desktop</summary>
         <description>
         If true, allows remote access to the desktop via the RFB
         protocol. Users on remote machines may then connect to the
         desktop using a VNC viewer.
         </description>
         <default>false</default>
      </key>
      ```
      
   * 左上搜尋 desktop sharing
   
      ![image](https://github.com/shift093/JetsonTX2NeedInstall/blob/master/jetson_setup.png)
      ![image](jetson_setup.png)

# 再試一試
      export DISPLAY=:1
      gsettings set org.gnome.Vino enabled true
      gsettings set org.gnome.Vino prompt-enabled false
      gsettings set org.gnome.Vino require-encryption false
      /usr/lib/vino/vino-server
      
# 完成

# 安裝tensorflow-gpu(aarch64)
      sudo apt install python3-pip 
      sudo apt install libhdf5-serial-dev hdf5-tools
      pip3 install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v42 tensorflow-gpu==1.13.1+nv19.X --user
      # pip 安裝都要加上`--user`
