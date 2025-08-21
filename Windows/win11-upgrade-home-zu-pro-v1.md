# Windows 11 Home-Lizenz entfernen & Pro aktivieren

`Anleitung erstellt: 21.8.2025`

`Anleitung getestet mit: 24H2`


# Problem: Windows-OEM-Lizenzen in UEFIs
- In manchen UEFIs, z.B. häufig in Laptops, werden OEM-Keys für die Windows Aktivierung gespeichert.
- Das hat zur Folge, dass Windows bei der Installation automatisch Windows-Home installiert, auch wenn man Pro nutzen möchte.
- Das Upgrade kann `ohne Neuinstallation` durchgeführt werden.


# 1. Home Lizenz entfernen
- Zunächst Windows-Home installieren.
- Danach OEM-Home-Key aus Windows entfernen:
	- Terminal in Windows nach der Installation als Admin starten.
	- Befehl ausführen, um Home-Lizenz zu entfernen.
```
$ slmgr /upk
```


--------------------------------------------------------------------------------------------------------------


# 2. Generischen Key um Pro zu aktivieren
- Generischen Key eingeben, um Upgrade von Home auf Windows-Pro durchzuführen:
	- Terminal in Windows als Admin starten
	- `VK7JG-NPHTM-C97JM-9MPGT-3V66T` > ist der Key für den Upgrade
	- Der Key dient `nur für den Upgrade`, `er aktiviert NICHT Windows`

```
$ changepk.exe /productkey VK7JG-NPHTM-C97JM-9MPGT-3V66T
```
- GGf. einen Neustart durchführen, um den Vorgang abzuschließen.

--------------------------------------------------------------------------------------------------------------


# 3. Produkt Schlüssel für Windows-Pro eingeben
- Pro Key eingeben:
	- Terminal in Windows als Admin starten
	- VVVVV-VVVVV-VVVVV-VVVVV-VVVVV mit dem eigenen Windows 11 Pro Produkt-Key ersetzen
```
$ changepk.exe /productkey VVVVV-VVVVV-VVVVV-VVVVV-VVVVV
```

- Alternativ in den Windows-Einstellungen unter `System > Aktivierung` den eigenen Pro-Key für Windows 11 eingeben.


--------------------------------------------------------------------------------------------------------------
