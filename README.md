# README - OpenBook E-Reader

**Autor: Artiom Pujleacov**

## Prezentare Generală

OpenBook este un dispozitiv e-reader open-source, bazat pe microcontrollerul ESP32-C6. Acesta integrează un ecran e-paper de 7.5 inch, senzori de mediu (BME680), un sistem de gestionare a bateriei și conectivitate prin Wi-Fi și USB-C. Acest document oferă detalii despre arhitectura hardware, componentele utilizate și conexiunile lor.

---

## Diagramă de Bloc

## Lista de Componente (BOM)

Tabelul de mai jos conține principalele componente utilizate, alături de link-uri către furnizori și fișele tehnice disponibile.

| **Componentă**       | **Part Number**               | **Descriere**                          | **Furnizor (Mouser)**                                                               | **Datasheet**                                                                                 |
|----------------------|------------------------------|----------------------------------------|------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| U2                  | ESP32-C6-WROOM-1-N8          | MCU Wi-Fi 6, Bluetooth 5              | [Mouser](https://eu.mouser.com/ProductDetail/Espressif-Systems/ESP32-C6-WROOM-1-N8) | [Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-c6-wroom-1_datasheet_en.pdf) |
| U1                  | W25Q512JVEIQ                 | Memorie Flash SPI 512Mb               | [Mouser](https://eu.mouser.com/ProductDetail/Winbond/W25Q512JVEIQ)                 | [Datasheet](https://www.winbond.com/resource-files/W25Q512JV%20RevD%2004082020.pdf)              |
| S                   | BME680                       | Senzor temperatură, umiditate, presiune | [Mouser](https://eu.mouser.com/ProductDetail/Bosch-Sensortec/BME680)               | [Datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme680-ds001.pdf) |

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
