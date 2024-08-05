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

## HIDBootloader
![HIDBootloader](https://github.com/SuperRockManZero/PIC18F2550-Bootloader/blob/main/Photo/p2.jpg)

## 使用說明
### 預先燒錄 Bootloader
使用 MPLAB X IDE 或燒錄工具將 [HEX](https://github.com/SuperRockManZero/PIC18F2550-Bootloader/blob/main/Code/production/Bootloader_PIC18F2550.production.hex) 檔案燒錄到 PIC18F2550 微控制器中。
### 使用者程式
設定 XC8 編譯器選項
1. 設定Codeoffset，如圖：
   ![Codeoffset](https://github.com/SuperRockManZero/PIC18F2550-Bootloader/blob/main/Photo/Required_Application_Project_Codeoffset_Linker_Settings_for_XC8.png)
2. 設定ROM ranges，如圖：
   ![ROM ranges](https://github.com/SuperRockManZero/PIC18F2550-Bootloader/blob/main/Photo/Required_Application_Project_ROM_Ranges_Linker_Settings_for_XC8.png)
### 硬體連接
1. 安排電源
    - 使用USB電源時；將VBUS與VCC連接，VUSB與VCC斷開。
    - 使用外接 5V 時；將VBUS與VCC斷開，VUSB與VCC斷開。
    - 不可使用 3.3V。
2. 將 RE3 引腳連接至GND
3. 開啟電源後即可進入Bootloader
### 更新使用者程式
1. 使用[HIDBootloader](https://github.com/SuperRockManZero/PIC18F2550-Bootloader/blob/main/Manual%20and%20Win%20APP/Win/HIDBootloader.exe)連接到 PIC18F2550 的USB口。將要更新的使用者程式 HEX 檔案傳送到 Bootloader。
2.  Bootloader 將接收並驗證，然後將其寫入微控制器的程式記憶體。
### 執行使用者程式
1. 斷開電源
2. 使 RE3 空接或連接至Vcc
3. 重新開啟電源即可執行使用者程式
### 限制
1. [config bit](https://github.com/SuperRockManZero/PIC18F2550-Bootloader/blob/main/Manual%20and%20Win%20APP/config_bit.txt) 不可更改
2. 不可使用 PIC18 擴展指令集
3. RE3 只能做為輸入引腳
4. RC0 在 Bootloader 期間為狀態指示輸出引腳

## 參考資料

## 貢獻
如果你有改進建議或發現問題，請提交 Issues 或 Pull Requests。

## 授權
此專案使用 [MIT 授權](LICENSE)。
