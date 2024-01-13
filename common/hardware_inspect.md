# 常用查看硬體指令 (Linux and FreeBSD)

## 注意
沒有特別寫哪個作業系統代表兩個作業系統都可以用

## File system
`mount`: 查看掛載的目錄

## Disk
`df -h`: disk free 的縮寫, -h = human readable format。

## Partition
`lsblk`: Linux, 列出所有 block device, 包括硬碟跟分區

`fdisk -l /dev/`: **Linux**, 列出特定裝置的分區，不同於 `lsblk`, `fdisk` 專門管理分區的指令。
fixed disk editor 的縮寫

`gpart show`: **FreeBSD**, 列出分區。geom partition 縮寫

## CPU
`lscpu`: 查看 CPU 硬體資訊

`sensors`，**Linux**, 用於檢測服務器內部降溫系統是否健康，可以監控主板，CPU 的工作電壓，風扇轉速、溫度等數據 - [man page](https://www.commandlinux.com/man-page/man1/sensors.1.html)

`sysctl hw.model`: **FreeBSD**, 查看 CPU 硬體資訊

`sysctl -a | grep temperature`: **FreeBSD**, 查看 CPU 溫度，通常在 sysctl 的 temperature 是用硬體內建的 sensor 來感知的

## Memory
`free -h`: free memory 的縮寫

`vmstat`: virtual memory statistics - [vmstat 監視內存使用情況](https://jasonblog.github.io/note/linux_tools/vmstat.html)

## GPU
`nvidia-smi`: Ubuntu, Nvidia 顯卡 info

`nvidia-setting`: Control panel of nvidia

## 系統資源使用率, Process info
`ps`: snapshot of current process usage

`top`: 查看系統資源，包括 PID, owner and CPU 使用率等各種其他資訊 - [Unix/Linux TOP 指令使用詳解](https://tigercosmos.xyz/post/2020/04/unix/top-usage/)

`htop`: `top` 強化板，需要自己額外安裝 - [你一定用過 htop，但你有看懂每個欄位嗎？](https://medium.com/starbugs/do-you-understand-htop-ffb72b3d5629)

`sysstate:`: **Linux** 開源工具，較關注歷史數據，並且可以深入分析，不熟悉 - [Sysstat：開源免費的 Linux 系統的監控工具](https://www.readfog.com/a/1630557928025067520)

## 其他硬體
1. `lshw`: **Linux**, list hardware，包括記憶體，音效卡，顯示卡等其他硬體資訊
2. `lsusb`: USB 硬體資訊
3. `dmidecode`: Direct Media Interface， 包括 BIOS、System、主機板等詳細的東西 - [用 dmidecode 查看 Linux 硬體資訊](https://shazi.info/%E7%94%A8-dmidecode-%E6%9F%A5%E7%9C%8B-linux-%E7%A1%AC%E9%AB%94%E8%B3%87%E8%A8%8A/)

## Reference
[常用查看硬體指令 (Linux and FreeBSD)](https://cozy-kola.medium.com/ubuntu-command-%E4%BE%86%E6%9F%A5%E7%9C%8B%E7%A1%AC%E9%AB%94%E8%B3%87%E8%A8%8A%E8%B7%9F%E4%BD%BF%E7%94%A8%E7%8E%87-299bbe58333c)