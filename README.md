# PIC18F2550 / PIC18LF2550 USB Bootloader
## 簡介
這個專案實現了一個 Bootloader，適用於 PIC18F2550 或 PIC18LF2550 微控制器。Bootloader 是一個小型引導裝載程式，允許你在不需要專用燒錄器的情況下，經由USB將新的使用者程式燒錄到微控制器中。

## 功能
- 透過 USB 接口接收和更新使用者程式
- 驗證接收到的使用者程式是否正確
- 簡化使用者程式更新流程

## Bootloader 原理

## 硬體要求
- PIC18F2550 或 PIC18LF2550 微控制器
- USB 通信接口

## 軟體要求
- MPLAB X IDE 或 MPLAB Xpress IDE
- XC8 編譯器
- HIDBootloader

## 使用說明
### 燒錄 Bootloader
  1. 使用 MPLAB X IDE 或燒錄工具將 [HEX](https://github.com/SuperRockManZero/PIC18F2550-Bootloader/blob/main/Code/production/Bootloader_PIC18F2550.production.hex) 檔案燒錄到 PIC18F2550 微控制器中。
### config bit
### XC8 編譯器的設定
### 硬體連接
 1. RE3連接至GND
 2. 開啟電源後即可進入Bootloader
### 更新使用者程式
  1. 使用[HIDBootloader](https://github.com/SuperRockManZero/PIC18F2550-Bootloader/blob/main/Manual%20and%20Win%20APP/Win/HIDBootloader.exe)連接到 PIC18F2550 的USB口。將要更新的使用者程式 HEX 檔案傳送到 Bootloader。
  2.  Bootloader 將接收並驗證，然後將其寫入微控制器的程式記憶體。
### 限制
 1. config bit 已固定
 2. 不可使用 PIC18 擴展指令集
 3. RE3 只能為輸入引腳
 4. RC0 在 Bootloader 期間為狀態指示輸出引腳

## 參考資料

## 貢獻
如果你有改進建議或發現問題，請提交 Issues 或 Pull Requests。

## 授權
此專案使用 [MIT 授權](LICENSE)。

**********************
1. 需先預燒錄 Bootloader_PIC18F2550.production.hex
2. 電源選擇
	a. 使用USB電源時；將VBUS與VCC連接，VUSB與VCC斷開。
	b. 使用本身所自帶 5V 電源時；將VBUS與VCC斷開，將VUSB與VCC斷開。
	c. 不可使用 3.3V 電源。
3. 於PC端執行 HIDBootloader.exe。
4. RE3連接至GND。再開啟自帶電源或連接USB。
5. 將使用者程式碼寫入。

使用者程式碼
1. 使用XC8編譯
	a. build configuration-->XC8 global options-->XC8 linker-->Option categories:Additional options
   	   將 "Codeoffset" 設為 0x1000
   	   參考圖片 "Required_Application_Project_Codeoffset_Linker_Settings_for_XC8.png"
	b. build configuration-->XC8 global options-->XC8 linker-->Option categories:Memory model,
   	   將 "ROM ranges" 設為 default,-0-FFF,-1006-1007,-1016-1017
	   參考圖片 "Required_Application_Project_ROM_Ranges_Linker_Settings_for_XC8.png"
1. 使用C18編譯
	a. 應加入 MLA 內的 "rm18f2550_g.lkr" 作為連接描述檔。(參考 PIC18F Bootloader Introduction V2.PDF)


附錄 : config bit 設定
	PLLDIV = 5       // PLL Prescaler Selection bits (Divide by 5 (20 MHz oscillator input))
	CPUDIV = OSC1_PLL2// System Clock Postscaler Selection bits ([Primary Oscillator Src: /1][96 MHz PLL Src: /2])
	USBDIV = 2       // USB Clock Selection bit (used in Full-Speed USB mode only; UCFG:FSEN = 1) (USB clock source comes from the 96 MHz PLL divided by 2)
	FOSC = HSPLL_HS  // Oscillator Selection bits (HS oscillator, PLL enabled (HSPLL))
	FCMEN = OFF      // Fail-Safe Clock Monitor Enable bit (Fail-Safe Clock Monitor disabled)
	IESO = OFF       // Internal/External Oscillator Switchover bit (Oscillator Switchover mode disabled)
	PWRT = ON        // Power-up Timer Enable bit (PWRT enabled)
	BOR = OFF        // Brown-out Reset Enable bits (Brown-out Reset disabled in hardware and software)
	BORV = 3         // Brown-out Reset Voltage bits (Minimum setting)
	VREGEN = ON      // USB Voltage Regulator Enable bit (USB voltage regulator enabled)
	WDT = OFF        // Watchdog Timer Enable bit (WDT disabled (control is placed on the SWDTEN bit))
	WDTPS = 32768    // Watchdog Timer Postscale Select bits (1:32768)
	CCP2MX = ON      // CCP2 MUX bit (CCP2 input/output is multiplexed with RC1)
	PBADEN = OFF     // PORTB A/D Enable bit (PORTB<4:0> pins are configured as digital I/O on Reset)
	LPT1OSC = OFF    // Low-Power Timer 1 Oscillator Enable bit (Timer1 configured for higher power operation)
	MCLRE = OFF      // MCLR Pin Enable bit (RE3 input pin enabled; MCLR pin disabled)
	STVREN = ON      // Stack Full/Underflow Reset Enable bit (Stack full/underflow will cause Reset)
	LVP = OFF        // Single-Supply ICSP Enable bit (Single-Supply ICSP disabled)
	XINST = OFF      // Extended Instruction Set Enable bit (Instruction set extension and Indexed Addressing mode disabled (Legacy mode))
	CP0 = OFF        // Code Protection bit (Block 0 (000800-001FFFh) is not code-protected)
	CP1 = OFF        // Code Protection bit (Block 1 (002000-003FFFh) is not code-protected)
	CP2 = OFF        // Code Protection bit (Block 2 (004000-005FFFh) is not code-protected)
	CP3 = OFF        // Code Protection bit (Block 3 (006000-007FFFh) is not code-protected)
	CPB = OFF        // Boot Block Code Protection bit (Boot block (000000-0007FFh) is not code-protected)
	CPD = OFF        // Data EEPROM Code Protection bit (Data EEPROM is not code-protected)
	WRT0 = OFF       // Write Protection bit (Block 0 (000800-001FFFh) is not write-protected)
	WRT1 = OFF       // Write Protection bit (Block 1 (002000-003FFFh) is not write-protected)
	WRT2 = OFF       // Write Protection bit (Block 2 (004000-005FFFh) is not write-protected)
	WRT3 = OFF       // Write Protection bit (Block 3 (006000-007FFFh) is not write-protected)
	WRTC = OFF       // Configuration Register Write Protection bit (Configuration registers (300000-3000FFh) are not write-protected)
	WRTB = OFF       // Boot Block Write Protection bit (Boot block (000000-0007FFh) is not write-protected)
	WRTD = OFF       // Data EEPROM Write Protection bit (Data EEPROM is not write-protected)
	EBTR0 = OFF      // Table Read Protection bit (Block 0 (000800-001FFFh) is not protected from table reads executed in other blocks)
	EBTR1 = OFF      // Table Read Protection bit (Block 1 (002000-003FFFh) is not protected from table reads executed in other blocks)
	EBTR2 = OFF      // Table Read Protection bit (Block 2 (004000-005FFFh) is not protected from table reads executed in other blocks)
	EBTR3 = OFF      // Table Read Protection bit (Block 3 (006000-007FFFh) is not protected from table reads executed in other blocks)
	EBTRB = OFF      // Boot Block Table Read Protection bit (Boot block (000000-0007FFh) is not protected from table reads executed in other blocks)
