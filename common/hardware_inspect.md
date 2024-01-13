# 常用查看硬體指令 (Ubuntu and FreeBSD)
## File system
`mount`: 查看掛載的目錄

## Disk
`df -h`: Ubuntu, disk free 的縮寫, -h = human readable format


## Partition
`lsblk`: Ubuntu, 列出所有 block device, 包括硬碟跟分區

`fdisk -l /dev/`: Ubuntu, 列出特定裝置的分區，不同於 `lsblk`, `fdisk` 專門管理分區的指令。
fixed disk editor 的縮寫

`gpart show`: FreeBSD, 列出分區。geom partition 縮寫

## CPU
`lscpu`: Ubuntu

`sysctl hw.model`: FreeBSD
`sysctl -a | grep temperature`: FreeBSD, CPU 溫度

## Memory
`free -h`: Ubuntu, free memory 的縮寫

## GPU
`nvidia-smi`: Ubuntu, Nvidia 顯卡 info
`nvidia-setting`: Control panel of nvidia

## 系統資源
`top`: 查看系統資源
`htop`: `top` 進階版，需要自己安裝

## Reference
[Ubuntu command 來查看硬體資訊跟使用率](https://cozy-kola.medium.com/ubuntu-command-%E4%BE%86%E6%9F%A5%E7%9C%8B%E7%A1%AC%E9%AB%94%E8%B3%87%E8%A8%8A%E8%B7%9F%E4%BD%BF%E7%94%A8%E7%8E%87-299bbe58333c)
[RPI4 with FreeBSD 15 Current](https://cozy-kola.medium.com/rpi4-with-freebsd-15-current-ac96f03e32df)