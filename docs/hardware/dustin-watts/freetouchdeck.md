# FreeTouchDeck

<div class="row justify-content-center">
        <a href="../images/freetouchdeck.jpg" data-toggle="lightbox" data-gallery="example-gallery" class="col-sm-6" data-title="FreeTouchDeck in 3D printed case" data-footer="Original image by Dustin Watts - Used with permission">
            <img src="../images/freetouchdeck.jpg" class="img-fluid">
        </a>

        <a href="../images/freetouchdeck-side.jpg" data-toggle="lightbox" data-gallery="example-gallery" class="col-sm-6" data-title="FreeTouchDeck in 3D printed case" data-footer="Original image by Dustin Watts - Used with permission">
            <img src="../images/freetouchdeck-side.jpg" class="img-fluid">
        </a>
</div>
<div>
        <a href="../images/freetouchdeck-bare.jpg" data-toggle="lightbox" data-gallery="example-gallery" rel="lightbox[work]" data-title="FreeTouchDeck PCB combiner with display" data-footer="Original image by Dustin Watts - Used with permission">more images...</a>
</div>

## Features

- ESP32 DevKitC (38pin)
- ILI9488 TFT SPI 4-WIRE
- XPT2046 resistive touch controller

This board is created for the [FreeTouchDeck project](https://github.com/DustinWatts/FreeTouchDeck){target=_blank}
and the [PCB-combiner board](https://www.pcbway.com/project/shareproject/ESP32_TFT_Combiner_V1.html){target=_blank} is open source. Due to the extensive documentation it was easy to port openHASP to the FreeTouchDeck.

| Pros               | Cons
|:-----              |:----
| 480x320 Display    | 4 MB flash
| Price              | No PSram
| [Build Instructions][1]{target=_blank} | Resistive touch

[1]: https://www.instructables.com/A-Bluetooth-ESP32-TFT-Touch-Macro-Keypad/

This is a kit so you need to assemble the parts yourself. Some soldering skills are required.
You can 3D print a custom enclosure.


## Product Video

<div class="embed-responsive embed-responsive-16by9" style="max-width:560px; margin:auto;">
    <iframe title="YouTube video player" src="https://www.youtube.com/embed/s2X4BQ9VmEU?rel=0&controls=1" class="embed-responsive-item" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen>
    </iframe>
</div>

## 3D Printed Cases

You can find a 3D printable case on [Thingiverse](https://www.thingiverse.com/thing:4661069){target=_blank}
and [Github](https://github.com/DustinWatts/FreeTouchDeck/tree/master/case/ESP32_TFT_Combiner_Case){target=_blank}.

<div class="row justify-content-center">
        <a href="../images/freetouchdeck-case1.jpg" data-toggle="lightbox" data-gallery="example-gallery" class="col-sm-4" data-title="FreeTouchDeck in 3D printed case" data-footer="Original image by Dustin Watts - Used with permission">
            <img src="../images/freetouchdeck-case1.jpg" class="img-fluid">
        </a>

        <a href="../images/freetouchdeck-case2.jpg" data-toggle="lightbox" data-gallery="example-gallery" class="col-sm-4" data-title="FreeTouchDeck in 3D printed case" data-footer="Original image by Dustin Watts - Used with permission">
            <img src="../images/freetouchdeck-case2.jpg" class="img-fluid">
        </a>

        <a href="../images/freetouchdeck-case3.png" data-toggle="lightbox" data-gallery="example-gallery" class="col-sm-4" data-title="FreeTouchDeck in 3D printed case" data-footer="Original image by Dustin Watts - Used with permission">
            <img src="../images/freetouchdeck-case3.png" class="img-fluid">
        </a>
</div>

## Flashing

The FreeTouchDeck can easily be flashed over USB like any ESP32 development board.

## GPIO Settings

These pins can be used freely as GPIOs:

## PCB Blueprint

The PCB Combiner is fully [Open Source Hardware](https://github.com/DustinWatts/ESP32_TFT_Combiner){target=_blank}:

- Schematics
- PCB layout

<a href="../images/freetouchdeck-pcb.png" data-toggle="lightbox" data-gallery="example-gallery" class="col-sm-4" data-title="FreeTouchDeck PCB Combiner" data-footer="Original image by Dustin Watts - Used with permission">
    <img src="../images/freetouchdeck-pcb.png" class="img-fluid">
</a>

## HASP build_flags

Specify the LCD Configuration to use and define the GPIOs in the environment build flags:

```ini linenums="1"
build_flags =
    ${env.build_flags}
    ${esp32.build_flags}

;region -- TFT_eSPI build options ------------------------
    -D USER_SETUP_LOADED=1
    -D ILI9488_DRIVER=1
    -D TFT_ROTATION=0 ; 0=0, 1=90, 2=180 or 3=270 degree
    -D TFT_WIDTH=320
    -D TFT_HEIGHT=480
    -D TFT_MISO=19    ; don't connect TFT SDO if other SPI devices share MISO
    -D TFT_MOSI=23
    -D TFT_SCLK=18
    -D TFT_CS=15      ; Chip select control pin
    -D TFT_DC=2       ; Data Command control pin
    -D TFT_RST=4      ; Reset pin (could connect to RST pin)
    -D TFT_BCKL=32    ; Default, configurable via web UI (e.g. 2 for D4)
    -D SUPPORT_TRANSACTIONS
    -D TOUCH_CS=21
    -D TOUCH_DRIVER=2046 ; XPT2606 Resistive touch panel driver
    -D SPI_FREQUENCY=27000000
    -D SPI_TOUCH_FREQUENCY=2500000
    -D SPI_READ_FREQUENCY=20000000
;endregion
```