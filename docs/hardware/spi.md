# SPI Protocol

SPI is een vrij eenvoudig protocol om data te verzenden tussen chips, op lage snelheid en over korte afstand.

Het protocol heeft een aantal verbindingen nodig die in het tabelletje hieronder staan uitgelegd.

|Afkorting|Naam|Functie|
|---------|----|-------|
|MOSI|Master Out Slave In|Op deze pin wordt de data gezet die van de master naar de slave gaat.
|MISO|Master In Slave Out|Op deze pin kan de slave data zetten die andersom van de slave naar de master gaat.
|CLK |Clock|Op deze pin staan de clock pulsen.
|CS  |Chip Select|Deze pin wordt laag getrokken als de chip geactiveerd moet worden.

Op de scope zit dit er als volgt uit. In dit voorbeeld worden meerdere bytes verzonden met een stukje Python code.

* De lichtblauwe lijn (CH2) is de CLK, het herhalende patroon is goed zichtbaar. Na acht pulsen vindt er een pauze plaats omdat er een tweede byte verzonden wordt.
* De gele lijn (CH1) is de MOSI en hier is bij de eerste byte het bitpatroon van de 0xAA te zien (0b10101010) en bij de tweede byte blijft hij laag omdat er 0b00000000 verzonden wordt.
* De donkerblauwe lijn (CH4) is de CS en geeft aan wanneer data verzonden wordt en dat de chip moet luisteren.
* In het groen eronder staat de gedecodeerde data zoals de scope het herkend.

![spi](images/spi_scope.jpg)

## Aansturen

Als de kernel module geladen is zijn er een of meer devices beschikbaar in `/dev/`, op een raspberry pi 4 ziet dat er als volgt uit.
Het is mogelijk om data rechstreeks naar deze devices te sturen bijvoorbeeld met `echo -n "aa" > /dev/spidev0.0` alleen gaat dit te snel voor de scope om op te pikken.

```
crw-rw----  1 root spi     153,   0 Mar 26 20:17 spidev0.0
crw-rw----  1 root spi     153,   1 Mar 26 20:17 spidev0.1
```

De Python spidev module gebruikt

```python
import spidev
import time

spi = spidev.SpiDev()
spi.open(0, 0)
spi.max_speed_hz = 100000

while True:
    spi.xfer2([0xAA, 0x00])
    time.sleep(0.1)
```

## Links

* [https://nl.wikipedia.org/wiki/Serial_Peripheral_Interface](https://nl.wikipedia.org/wiki/Serial_Peripheral_Interface)
* [https://en.wikipedia.org/wiki/Serial_Peripheral_Interface](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface)
