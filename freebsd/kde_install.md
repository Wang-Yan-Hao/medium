# FreeBSD 安裝桌面環境 (x11 + KDE Plasma)


1. `pkg install xorg` 安裝 Xorg
2. `pw groupmod video -m [user]` 把預計使用桌面的使用者設成 video 群組，使用 `id -Gn [user]` 來查看 user 屬於的群組
3. `pciconf -lv|grep -B4 VGA` 查看電腦使用的顯卡，我是在 VMware 上安裝的，所以會顯示 Virtual Machine Communication Interface
4. `pkg install xf86-video-vmware` 根據顯卡，安裝對應的驅動程式，如果是在實體顯卡上，則需要在 Xorg 的設定檔 (/usr/local/etc/X11/xorg.conf.d/) 加入驅動路徑，詳情請看手冊，虛擬機不需要驅動
5. `pkg install kde5` 安裝 KDE
6. `sysrc dbus_enable=”YES”` 開機時自動啟動 DBus
    ![image](https://hackmd.io/_uploads/S1pSC-cFa.png)
    
    from [wiki](https://zh.wikipedia.org/zh-tw/D-Bus)
    
    sysrc 把後面的字串寫入到 /etc/rc.conf，此文件為開機時系統的配置文件，可以設定開機時開啟各種系統服務，使用 shell 編寫
7. `sysctl net.local.stream.recvspace=65536`
    `sysctl net.local.stream.sendspace=65536`
    sysctl 設定核心的系統參數，而不需要重開機就能套用 (etc/sysctl.conf)，此為提高一些 local stream socket communication buffer 的大小，有助於提高效能。使用 sysctl 只是暫時的，關係後設定就會消失，所以要直接設定 sysctl.conf
8. `echo “exec ck-launch-session startplasma-x11” > ~/.xinitrc`
~/.xinitrc 是 X window 在開啟時會執行的檔案，因此 exec ck-launch-session startplasma-x11 代表設定一個 ConsoleKt session，然後開啟 KED Plasma
9. `startx` 開啟 X window, 會直接執行 KED Plasma

## 踩到的坑
我在剛打開 KDE 時 (VMware)，整個畫面都超大，導致滑鼠跟鍵盤都變得超卡，無法操作，好像解析度有點問題 (超出 1920x1080了)，但都無法設定。

最後發現好像跟 VMware 的設定有關係，我把它從 Use host setting 改成 Specify setting 後，它才恢復正常，不然原本無法透過裡面的 KDE or X window 來設定解析度。

![image](https://hackmd.io/_uploads/BJ1vbGqY6.png)


還有安裝 chromium 有時後會遇到無法安裝的情況，是因為 pkg repo 版本的問題，請參考[討論](https://forums.freebsd.org/threads/chromium-disappeared-from-pkg-after-upgrade.87491/)

並且安裝 chromium 請在安裝 noto (`pkg install noto`)，才可以顯示中文


## Reference
* [Chapter 5. The X Window System](https://docs.freebsd.org/en/books/handbook/x11/)
* [Chapter 8. Desktop Environments](https://docs.freebsd.org/en/books/handbook/desktop/)
