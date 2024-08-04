# PIC18F2550/PIC18LF2550 USB Bootloader

## 簡介
這個專案實現了一個 Bootloader，適用於 PIC18F2550 或 PIC18LF2550 微控制器。Bootloader 是一個小型程式，允許你在不需要專用燒錄器的情況下，通過USB將新的固件燒錄到微控制器中。

## 功能
- 透過 USB 接口接收和更新固件
- 驗證接收到的固件是否正確
- 支援固件版本升級
- 簡化固件更新流程

## 硬體要求
- PIC18F2550 或 PIC18LF2550 微控制器
- USB 通信接口
- 固件更新程式

## 軟體要求
- MPLAB X IDE 或 MPLAB Xpress IDE
- XC8 編譯器
- HIDBootloader

## 使用說明

  ### 硬體連接

  ### 燒錄 Bootloader
1. 使用 MPLAB X IDE 或燒錄工具將 [HEX](https://github.com/SuperRockManZero/PIC18F2550-Bootloader/blob/main/Code/production/Bootloader_PIC18F2550.production.hex) 檔案燒錄到 PIC18F2550 微控制器中。

  ### 更新固件
1. 使用[HIDBootloader](https://github.com/SuperRockManZero/PIC18F2550-Bootloader/blob/main/Manual%20and%20Win%20APP/Win/HIDBootloader.exe)連接到 PIC18F2550 的USB口。
2. 將要更新的固件 HEX 檔案發送到 Bootloader。
3. Bootloader 將接收並驗證固件，然後將其寫入微控制器的程式記憶體。

  ### config bit

## 參考資料

## 貢獻
如果你有改進建議或發現問題，請提交 Issues 或 Pull Requests。

## 授權

此專案使用 [MIT 授權](LICENSE)。
