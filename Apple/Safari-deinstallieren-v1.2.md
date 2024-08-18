# [Safari](https://www.apple.com/de/safari/) deinstallieren


`Anleitung verfasst am 8.12.2023`

`für die Anleitung verwendetes Betriebssystem: MacOS Sonoma`



### Einen Intel-Mac im Wiederherstellungsmodus neu starten:

- Den Mac ausschalten.
- `Ein/Aus-Taste` drücken und `Befehl-R` gedrückt halten.
- Warten, bis das Apple-Logo erscheint und dann `Befehl-R` los lassen.
- Nun sollte das Fenster macOS-Dienstprogrammen zu sehen sein.

- über die obere Leiste auf `Dienstprogramme` klicken und das Terminal öffnen und Befehl einfügen:
```
$ csrutil disable
```
- Mac neu starten



### Terminal öffnen:

```
$ cd /Applications/
```
```
$ sudo rm -rf Safari.app/
```


### Nach der Deinstallation von der Safari App:

- Den Mac ausschalten.
- `Ein/Aus-Taste` drücken und `Befehl-R` gedrückt halten.
- Warten, bis das Apple-Logo erscheint und dann `Befehl-R` los lassen.
- Nun sollte das Fenster macOS-Dienstprogrammen zu sehen sein.

- Über die obere Leiste auf `Dienstprogramme` klicken und das Terminal öffnen und Befehl einfügen:
```
$ csrutil enable
```
- Mac neu starten.


-----------------------------------------------------------------------------------------------------------------
