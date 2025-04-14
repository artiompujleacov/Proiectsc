# README - OpenBook E-Reader

**Autor: Artiom Pujleacov**

## Prezentare Generală

OpenBook este un dispozitiv e-reader open-source, bazat pe microcontrollerul ESP32-C6. Acesta integrează un ecran e-paper de 7.5 inch, senzori de mediu (BME680), un sistem de gestionare a bateriei și conectivitate prin Wi-Fi și USB-C. Acest document oferă detalii despre arhitectura hardware, componentele utilizate și conexiunile lor.

---

## Diagramă de Bloc

![image](https://github.com/user-attachments/assets/73321fdc-fcb5-4e21-9802-32a2912f6943)



# Lista de componente

| Cantitate | Componentă                         | Valoare | Descriere                                 | Carcasă                         | Reper        | Link Cumpărare                                                                 | Datasheet                                                                          |
|-----------|------------------------------------|---------|-------------------------------------------|---------------------------------|--------------|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| 1         | ADAFRUIT_LEDCHIP-LED0603           | -       | LED                                       | ADAFRUIT_CHIP-LED0603           | CHG_LED      | [link](https://www.mouser.com/ProductDetail/Adafruit/CHIP-LED0603)               | [datasheet](https://www.mouser.com/datasheet/2/737/CHIP-LED0603-1877199.pdf)       |
| 1         | SJ                                 | -       | SMD solder JUMPER                         | SJ                              | SJ1          | [link](https://www.mouser.com/ProductDetail/TE-Connectivity/1-2176091-2)         | [datasheet](https://www.mouser.com/datasheet/2/418/1-2176091-2-1817091.pdf)        |
| 1         | ESP32_WROVER_EAGLE-LTSPICE_RR0402  | 0.47Ω   | Rezistor                                  | ESP32_WROVER_EAGLE-LTSPICE_R0402| R3           | [link](https://www.mouser.com/ProductDetail/Vishay/CRCW04020047ZRT7)             | [datasheet](https://www.mouser.com/datasheet/2/427/crcwce-1764191.pdf)             |
| 1         | ESP32_WROVER_EAGLE-LTSPICE_RR0402  | 100KΩ   | Rezistor                                  | ESP32_WROVER_EAGLE-LTSPICE_R0402| R1_PWRUSB    | [link](https://www.mouser.com/ProductDetail/Vishay/CRCW0402100KFKED)             | [datasheet](https://www.mouser.com/datasheet/2/427/crcwce-1764191.pdf)             |
| 8         | EAGLE-LTSPICE_CC0402               | 100nF   | Condensator                               | EAGLE-LTSPICE_C0402             | C1, C2, C4_USB, C6, C8, C9, C10, C_DELAY | [link](https://www.mouser.com/ProductDetail/Murata/GRM155R71C104KA88D)            | [datasheet](https://www.mouser.com/datasheet/2/281/GRM155R71C104KA88D-1767201.pdf) |
| 1         | RCL_CPOL-EUCT3528                  | 100µF   | Condensator polarizat                     | RCL_CT3528                      | C3           | [link](https://www.mouser.com/ProductDetail/Panasonic/EEE-FK1V101P)              | [datasheet](https://www.mouser.com/datasheet/2/315/EEE-FK1V101P-1526881.pdf)       |
| 10        | ESP32_WROVER_EAGLE-LTSPICE_RR0402  | 10KΩ    | Rezistor                                  | ESP32_WROVER_EAGLE-LTSPICE_R0402| R1, R1-PINH, R1_PINH1, R2-PINH, R2_PINH1, R4, R_BOOT, R_CHANGE, R_CL1, R_RESET | [link](https://www.mouser.com/ProductDetail/Vishay/CRCW040210K0FKED)              | [datasheet](https://www.mouser.com/datasheet/2/427/crcwce-1764191.pdf)             |
| 6         | ESP32_WROVER_EAGLE-LTSPICE_RR0402  | 10kΩ    | Rezistor                                  | ESP32_WROVER_EAGLE-LTSPICE_R0402| R5, R6, R7, R8, R9, R10 | [link](https://www.mouser.com/ProductDetail/Vishay/CRCW040210K0FKED)              | [datasheet](https://www.mouser.com/datasheet/2/427/crcwce-1764191.pdf)             |
| 1         | EAGLE-LTSPICE_CC0402               | 10µF    | Condensator                               | EAGLE-LTSPICE_C0402             | C7           | [link](https://www.mouser.com/ProductDetail/Murata/GRM155R61A106ME44D)           | [datasheet](https://www.mouser.com/datasheet/2/281/GRM155R61A106ME44D-1767201.pdf) |
| 1         | 112A-TAAR-R03_ATTEND               | -       | Micro SD Card Socket, Push-Push Type      | 112ATAARR03ATTEND               | J4           | [link](https://www.mouser.com/ProductDetail/Attend/112A-TAAR-R03)                | [datasheet](https://www.mouser.com/datasheet/2/828/112A-TAAR-R03-1222862.pdf)      |
| 1         | ESP32_WROVER_EAGLE-LTSPICE_RR0402  | 15Ω     | Rezistor                                  | ESP32_WROVER_EAGLE-LTSPICE_R0402| R_CAPACITOR  | [link](https://www.mouser.com/ProductDetail/Vishay/CRCW040215R0FKED)             | [datasheet](https://www.mouser.com/datasheet/2/427/crcwce-1764191.pdf)             |
| 1         | EAGLE-LTSPICE_CC0402               | 1µF     | Condensator                               | EAGLE-LTSPICE_C0402             | C5           | [link](https://www.mouser.com/ProductDetail/Murata/GRM155R61A105KE15D)           | [datasheet](https://www.mouser.com/datasheet/2/281/GRM155R61A105KE15D-1767201.pdf) |
| 10        | EAGLE-LTSPICE_CC0402               | 1µF/50V | Condensator ceramic multi-strat           | 0402                           | EPD_C1, EPD_C2, EPD_C5, EPD_C6, EPD_C7, EPD_C8, EPD_C9, EPD_C10, EPD_C11, EPD_C12 | [link](https://www.mouser.com/ProductDetail/Murata-Electronics/GRM155R61A105KE15D) | [datasheet](https://www.mouser.com/datasheet/2/281/1/GRM155R61A105KE15_01A-1983730.pdf) |


---

## Detalii Hardware

### ESP32-C6-WROOM-1-N8

- **Rol**: Control principal, suport pentru conectivitate wireless și periferice.
- **Interfețe disponibile**:
  - SPI: Display e-paper, memorie Flash, card Micro SD.
  - I2C: Senzor BME680, monitorizare baterie (MAX17048), ceas RTC (DS3231).
  - GPIO: Interacțiune cu butoane și LED-uri.
  - UART: Debugging și conectivitate serială.
- **Specificații**: 160MHz, 512KB SRAM, 8MB Flash integrat.

### Display E-Paper

- **Caracteristici**: Dimensiune 7.5 inch, rezoluție 800x480 pixeli, contrast 8:1.
- **Conectivitate**: Utilizare prin interfață SPI cu linii dedicate pentru control și resetare.
- **Consum**: <50mA în timpul actualizării imaginii, aproape nul în mod standby.

### Senzor BME680

- **Funcționalitate**: Măsurători de temperatură, umiditate, presiune atmosferică și calitate a aerului.
- **Interfață**: Conectare prin magistrala I2C la 400kHz.
- **Consum**: Sub 1mA în activitate, sub 1µA în modul de repaus.

### Sistem de Alimentare

- **Baterie**: Li-Po de 2500mAh, 3.7V.
- **Încărcare**: Controlată de MCP73831 prin portul USB-C, cu o capacitate maximă de 1A.
- **Monitorizare**: Funcție asigurată de MAX17048, comunicare prin I2C.
- **Consum energetic**:
  - Activ (Wi-Fi + ecran actualizat): ~150mA.
  - Standby (doar ecran afișat): ~10mA.
  - Deep Sleep: Sub 50µA.
  - **Autonomie estimată**: Aproximativ o săptămână (~250 ore cu un consum mediu de 10mA).

### Butoane de Navigare

- Echipate cu butoane tactile Panasonic EVQPUJ02K, fiecare având o rezistență pull-up de 10KΩ.

### USB-C

- **Rol**: Funcționează atât pentru încărcare (5V/1A), cât și pentru transfer de date (USB 2.0).
- **Protecție**: Integrare de diode ESD (USBLC6-2SC6Y) pentru siguranță la supratensiune.

---

## Configurare Pini ESP32-C6

| **Pin ESP32-C6** | **Funcție**         | **Componentă**         | **Rol**                                    |
|------------------|--------------------|------------------------|--------------------------------------------|
| GPIO0           | BOOT_BUTTON        | Buton                  | Mod boot la inițializare                   |
| GPIO1           | RESET_BUTTON       | Buton                  | Reset manual                               |
| GPIO2           | CHANGE_BUTTON      | Buton                  | Schimbare meniuri                          |
| GPIO3           | EPD_CS             | Display E-Paper        | Chip Select pentru SPI                     |
| GPIO4           | EPD_DC             | Display E-Paper        | Control Date/Comenzi                       |
| GPIO5           | EPD_RST            | Display E-Paper        | Reset display                              |
| GPIO6           | EPD_BUSY           | Display E-Paper        | Detectare stare refresh                    |
| GPIO7           | SPI_MOSI           | Display, Flash, SD     | Linii de date SPI                          |
| GPIO8           | SPI_MISO           | Display, Flash, SD     | Linie de date SPI (citire)                 |
| GPIO9           | SPI_SCK            | Display, Flash, SD     | Semnal de ceas SPI                         |
| GPIO10          | FLASH_CS           | Memorie Flash          | Chip Select pentru memorie                 |
| GPIO11          | SD_CS              | Card Micro SD          | Chip Select pentru card SD                 |
| GPIO12          | I2C_SDA            | BME680, MAX17048, DS3231 | Linie de date pentru I2C                   |
| GPIO13          | I2C_SCL            | BME680, MAX17048, DS3231 | Linie de ceas pentru I2C                   |
| GPIO14          | CHG_LED            | LED                    | Indică procesul de încărcare               |
| GPIO15          | UART_TX            | Debugging              | Transmitere date seriale                    |
| GPIO16          | UART_RX            | Debugging              | Recepție date seriale                       |
| GPIO17          | USB_D+             | USB-C                  | Linie de date USB pozitivă                  |
| GPIO18          | USB_D-             | USB-C                  | Linie de date USB negativă                  |

**Notă**: Pinii sunt selectați conform specificațiilor ESP32-C6 și funcționalităților necesare dispozitivului OpenBook. Unele dintre aceștia sunt multifuncționali și pot fi reutilizați în diverse configurații.

---
