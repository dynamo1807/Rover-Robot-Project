# Firmware

Die produktive Firmware wurde noch nicht initialisiert. MR-011 wählt das
Buildsystem aus und richtet ein reproduzierbares STM32G431-Projekt ein, bevor
die Funktionsentwicklung beginnt.

Die vorgesehenen Schichten, der Sicherheitszustandsautomat, die
Programmierrichtlinien und die Verifikationsstrategie sind in
[`docs/FIRMWARE.md`](../docs/FIRMWARE.md) dokumentiert.

Nicht ausschließlich erzeugte IDE-Ausgaben committen. Das Repository muss die
Eingaben enthalten, die für einen sauberen, reproduzierbaren Build erforderlich
sind, einschließlich Werkzeugkettenversion und Grenzen des generierten Codes.
