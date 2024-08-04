# PIC18F2550 Bootloader

## 簡介

這個專案實現了一個 Bootloader，適用於 PIC18F2550 微控制器。Bootloader 是一個小型程式，允許你在不需要專用燒錄器的情況下，通過串口 (UART) 將新的固件燒錄到微控制器中。這樣可以簡化固件更新過程，尤其是在產品部署後。

## 功能

- 透過 UART 接口接收和更新固件
- 驗證接收到的固件是否正確
- 支援固件版本升級
- 簡化固件更新流程

## 硬體要求

- PIC18F2550 微控制器
- 串口 (UART) 通信接口
- 配套的固件更新程式

## 軟體要求

- MPLAB X IDE 或 MPLAB Xpress IDE
- XC8 編譯器

## 使用說明

### 硬體連接

1. 將 PIC18F2550 的 TX 和 RX 引腳分別連接到電腦的串口接口。
2. 確保其他必要的電源和接地線連接已經完成。

### 編譯 Bootloader

1. 使用 MPLAB X IDE 打開 Bootloader 專案。
2. 確保選擇了正確的目標設備 (PIC18F2550) 和編譯器 (XC8)。
3. 編譯專案以生成 Bootloader 的 HEX 檔案。

### 燒錄 Bootloader

1. 使用 MPLAB X IDE 或其他燒錄工具將編譯生成的 HEX 檔案燒錄到 PIC18F2550 微控制器中。

### 更新固件

1. 使用串口通信工具（如 PuTTY 或 Tera Term）連接到 PIC18F2550 的串口。
2. 將要更新的固件 HEX 檔案發送到 Bootloader。
3. Bootloader 將接收並驗證固件，然後將其寫入微控制器的程式記憶體。

## 配置選項

Bootloader 支援一些基本的配置選項，這些選項可以通過修改原始碼中的設定常數來設定：

- `BAUD_RATE`: 設定串口通信的波特率
- `FIRMWARE_START_ADDRESS`: 固件開始存儲的地址
- `APPLICATION_START_ADDRESS`: 應用程式開始的地址

## 常見問題

**Q: 如何知道 Bootloader 是否成功接收到固件？**

A: Bootloader 通常會發送確認訊息到串口，你可以在串口通信工具中查看這些訊息。

**Q: 如果固件更新失敗怎麼辦？**

A: 如果固件更新失敗，Bootloader 通常會保留先前的固件，並嘗試重新啟動。請檢查固件檔案是否正確以及通信連接是否穩定。

## 參考資料

- [PIC18F2550 數據手冊](https://www.microchip.com/wwwproducts/en/PIC18F2550)
- [MPLAB X IDE 文件](https://www.microchip.com/mplab/mplab-x-ide)
- [XC8 編譯器手冊](https://www.microchip.com/mplab/compilers)

## 貢獻

如果你有改進建議或發現問題，請提交 Issues 或 Pull Requests。

## 授權

此專案使用 [MIT 授權](LICENSE)。
