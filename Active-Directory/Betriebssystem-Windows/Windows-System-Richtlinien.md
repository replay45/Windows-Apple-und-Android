# Windows-System/Systemsteuerung-Richtlinien

`Anleitung verfasst am 4.12.2025`

`Windows-Server - Active Directory`


----------------------------------------------------------------------------------------

# System

## Anmelden
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > System > Anmelden`
- `Animation bei der ersten Anmeldung anzeigen` -> Deaktiviert (Anzeige von Animationen & Anmeldeaufforderung an Benutzer für MS-Dienste)
- `Anmeldung mit Bildcode Deaktivieren` -> Aktiviert (Aktivierung von Richtlinie, deaktiviert, dass Nutzer sich mit einem Bild welches lokal gespeichert ist anmelden können)
- `Komfortable PIN-Anmeldung aktivieren` -> Dektiviert (Windows Hello-PIN)

----------------------------------------------------------------------------------------

## Benutzerprofile (WerbeID deaktivieren)
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > System > Benutzerprofile`
- `WerbeID deaktivieren` -> Aktiviert (Richtlinie aktivieren um WerbeID zu deaktivieren, WerbeID ist eine ID um Nutzer genau zu tracken und Analysen anzufertigen, sollte unbedingt deaktiviert werden!)

----------------------------------------------------------------------------------------

## Betriebssystemrichtlinien
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > System > Betriebssystemrichtlinien`
- `Aktivitätsfeed aktivieren` -> Deaktiviert (keine Veröffentlichug und Cloudsyncronisierung des Aktivitätsfeeds)
- `Syncronisierung der Zwischenablage geräteübergreifend zulassen` -> Deaktiviert (keine Cloudsyncronisierung der Zwischenablage)
- `Upload von Benutzeraktivitäten zulassen` -> Deaktiviert (keine Hochladung von Benutzeraktivitäten)
- `Veröffentlichen von Benutzeraktivitäten zulassen` -> Deaktiviert (keine Veröffentlichung von Benutzeraktivitäten)

----------------------------------------------------------------------------------------

## Energieverwaltung 

### "Verhalten des Netzschalters" (Energieoptionen) in Windows
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > System > Energieverwaltung > Schaltflächeneinstellungen`
- `Netzschalteraktion auswählen (Netzbetrieb)` -> Aktiviert, Wert: `Herunterfahren`
- `Aktion für Standbyschalter auswählen (Netzbetrieb)` -> ggf. Aktiviert, Wert: `Standbymodus`
- `Aktion für Netzschaltersymbol im Startmenü auswählen (Netzbetrieb)` -> ggf. Aktiviert, Wert: `Herunterfahren`
- `Gewünschte Aktion beim Schließen des Deckels auswählen (Netzbetrieb)` -> ggf. Aktiviert, Wert: `Ruhezustand`
- `Netzschalteraktion auswählen (Akkubetrieb)` -> ggf. Aktiviert, Wert: `Herunterfahren`
- `Aktion für Standbyschalter auswählen (Akkubetrieb)` -> ggf. Aktiviert, Wert: `Standbymodus`
- `Aktion für Netzschaltersymbol im Startmenü auswählen (Akkubetrieb)` -> ggf. Aktiviert, Wert: `Herunterfahren`
- `Gewünschte Aktion beim Schließen des Deckels auswählen (Akkubetrieb)` -> ggf. Aktiviert, Wert: `Ruhezustand`

### Standbymoduseinstellungen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > System > Energieverwaltung > Standbymoduseinstellungen`
- `Kennwortanfordern, wenn ein Computer reaktiviert wird (Akkubetrieb)` -> Aktiviert
- `Kennwortanfordern, wenn ein Computer reaktiviert wird (Netzbetrieb)` -> Aktiviert

----------------------------------------------------------------------------------------

# Systemsteuerung

## Anpassung
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Systemsteuerung > Anpassung`
- `Aktivieren der Diashow auf dem Sperrbildschirm verhindern` -> Aktiviert
- `Ein bestimmtes Standardbild für den Sperr- und Anmeldebildschirm erzwingen` -> Aktiviert, Nur für Windows Enterprise/ Education/Server verfügbar
- `Sperrbildschirmhintergrundanimation verhindern` -> Aktiviert

----------------------------------------------------------------------------------------
