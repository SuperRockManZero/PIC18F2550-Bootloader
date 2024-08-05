# PIC18F2550 / PIC18LF2550 USB Bootloader
## 簡介
這個專案實現了一個 Bootloader，適用於 PIC18F2550 或 PIC18LF2550 微控制器。Bootloader 是一個小型引導裝載程式，允許你在不需要專用燒錄器的情況下，經由USB將新的使用者程式燒錄到微控制器中。

## 功能
- 透過 USB 接口接收和更新使用者程式
- 驗證接收到的使用者程式是否正確
- 簡化使用者程式更新流程

## 硬體要求
- PIC18F2550 或 PIC18LF2550 微控制器
- USB 通信接口

## 軟體要求
- MPLAB X IDE 或 MPLAB Xpress IDE
- XC8 編譯器
- HIDBootloader

## 使用說明

#### 燒錄 Bootloader
  1. 使用 MPLAB X IDE 或燒錄工具將 [HEX](https://github.com/SuperRockManZero/PIC18F2550-Bootloader/blob/main/Code/production/Bootloader_PIC18F2550.production.hex) 檔案燒錄到 PIC18F2550 微控制器中。
#### config bit
#### 硬體連接
#### 更新使用者程式
  1. 使用[HIDBootloader](https://github.com/SuperRockManZero/PIC18F2550-Bootloader/blob/main/Manual%20and%20Win%20APP/Win/HIDBootloader.exe)連接到 PIC18F2550 的USB口。
  2. 將要更新的使用者程式 HEX 檔案傳送到 Bootloader。
  3. Bootloader 將接收並驗證，然後將其寫入微控制器的程式記憶體。

## 參考資料

## 貢獻
如果你有改進建議或發現問題，請提交 Issues 或 Pull Requests。

## 授權
此專案使用 [MIT 授權](LICENSE)。
