# FreeBSD 在 KDE 桌面使用 USB webcam
## Step
1. `pkg install webcamd`: webcamd 是一個 daemon, userspace application, 負責支援使用基於 USB 的 webcam 和 DVB USB 裝置
2. `pkg install pwcview`: 使用 webcam 的應用程式
3. `sysrc webcamd_enable="YES"`: 在開機的時候自動啟動 webcamd, 會把後者字串寫到 /etc/rc.conf, rc 的意思是 run command
4. `pw groupmod webcamd -m [username]`: 加入 user 到 webcamd group, 讓 user 不需要 root 就能使用 webcamd
5. `kldload cuse`: FreeBSD kernel module, 負責創建 character device (像是鍵盤滑鼠, 這邊就是要創建 webcam 的 device, /dev/video0)，webcamd 需要此 module 創建 webcamd character device
6. `webcamd -l`: 列出可以用的 usb 裝置，使用 `sysrc webcamd_0_flags=""` 指定要使用的 USB 裝置  
例如 `sysrc webcamd_0_flags="-d ugen0.2"`
7. `service webcamd start`: 開啟 webcamd 服務
8. 現在你因該可以使用 `pwcview` 來使用 webcam 了

要讓瀏覽器使用 webcam 需要多一點步驟，因為瀏覽器在 FreeBSD 使用 Video4Linux 框架，所以要在多安裝一點東西。

![image](https://hackmd.io/_uploads/BJPHsnpKa.png)

1. `pkg install v4l-utils v4l_compat`

可以在 [Webcam Test](https://www.google.com/search?q=webcamd+test+oneline&oq=webcamd+test+oneline&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIJCAEQABgNGIAEMggIAhAAGA0YHjIICAMQABgNGB4yCAgEEAAYDRgeMggIBRAAGA0YHjIICAYQABgNGB4yCAgHEAAYDRgeMggICBAAGA0YHjIICAkQABgNGB7SAQgyNDg4ajBqN6gCALACAA&sourceid=chrome&ie=UTF-8) 網站測試是否能在瀏覽器使用

## 遇到的坑
1. 執行 pwcview 會有資源不夠錯誤，原本以為是 X window 獲得到的記憶體不夠，使用 [xorg.conf](https://man.freebsd.org/cgi/man.cgi?query=xorg.conf&apropos=0&sektion=0&manpath=FreeBSD+10.1-RELEASE+and+Ports&arch=default&format=html) 來設定 X window 能使用的 memory (VideoRam	 mem)，但還是不能用，最重益的是 xorg.conf 在 FreeBSD 11 之後的 man page 就沒有了，所以不確定能不能用。  
最後發現只要把桌面大小設小一點，不要 1920 x 1080，就可以用了，還是不太知道確切的原因，可能桌面小一點就有足夠的資源了？  
但應該不影響瀏覽器使用 webcam
2. 我是使用 VMware player 的 USB passthorugh 來使用攝影機，但要注意設定 USB 相容性 (USB Compatibility)，建議直接設定 USB 3.0，我因為沒注意到，一直設成 1.0，所以一直沒辦法使用，甚至不知道為什麼我的 webcam 是 usb2.0，還是要設成 3.0 才可以在虛擬機使用。
![image](https://hackmd.io/_uploads/SJD-026F6.png)
image from [How to connect USB 3.0 devices in VMware WorkStation Pro VM](https://www.how2shout.com/how-to/how-to-connect-usb-3-0-devices-vmware-workstation-pro-virtual-machine.html)


## Reference
* [Chapter 9. Multimedia](https://docs.freebsd.org/en/books/handbook/multimedia/)
* [How to configure FreeBSD to use a webcam (version 12 and 13)](https://www.adminbyaccident.com/freebsd/how-to-freebsd/how-to-configure-freebsd-to-use-a-webcam-version-12-and-13/)