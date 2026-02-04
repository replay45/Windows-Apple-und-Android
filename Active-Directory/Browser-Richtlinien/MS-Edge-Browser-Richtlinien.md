# [MS-Edge](https://www.microsoft.com/de-de/edge/download?ch=1&form=MA13FJ) über GPO Richtlinien konfigurieren - Active Directory

`Anleitung verfasst am 8.4.2025, zuletzt bearbeitet am 6.1.2026`

`Windows-Server - Active Directory`


-------------------------------------------------------------------------------------------------------------


## MS-Edge zentral von allen Clients entfernen/ Ausführung des Programms verbieten

- Wie der Microsoft Edge über GPO Richtlinie auf allen Clients `deinstalliert` oder in eine `Art "Kiosk-Modus"` versetzt werden kann, wird in der Anleitung [MS-Edge einschränken oder deinstallieren](https://github.com/replay45/Windows-Apple-und-Android/tree/main/Active-Directory/Browser-konfigurieren) erklärt.

- Wie man die Ausführung bestimmter Programme verhindern kann, wird in der Anleitung [Ausführung-von-Programmen-verhindern](https://github.com/replay45/Windows-Apple-und-Android/tree/main/Active-Directory/Software-%26-Programme) erklärt.


-------------------------------------------------------------------------------------------------------------


### ADMX/ADML-Vorlagen herunterladen und importieren
- Zunächst müssen natürlich die Vorlagen für den MS-Edge in Active-Directory Server hinzugefügt werden, damit die Einstellungen vorgenommen werden können.
- [Vorlagen herunterladen](https://www.microsoft.com/en-us/edge/business/download?ch=1&cs=3515903432&form=MA13FJ) und entpacken

- Wofür sind die Dateien ?
	- .admx → Enthält die eigentlichen Richtlinien (Regeln & Einstellungen)
	- .adml → Enthält die sprachspezifischen Beschreibungen für die Benutzeroberfläche

- Für eine Domäne (Active Directory):
	- Windows Explorer auf AD-Server öffnen
	- Wenn der Ordner `PolicyDefinitions` in dem einzufügenden Pfad fehlt, einfach anlegen und innerhalb des Ordners den Ordner `de-DE` erstellen.
	- folgenden Pfad aus der entpackten Datei öffnen: `/MSEdgePolicyTemplates/windows/admx/`
	- alle `.admx`-Dateien in folgenden Pfad kopieren: `\\DomainController\SYSVOL\Domain\Policies\PolicyDefinitions\`
	- alle `.adml`-Dateien in folgenden Pfad kopieren: `\\DomainController\SYSVOL\Domain\Policies\PolicyDefinitions\de-DE\`



### Gruppenrichtlinienverwaltung öffnen
- `gpmc.msc`
- Neues Gruppenrichtlinienobjekt anlegen
	- Rechtsklick auf `Gruppenrichtlinienobjekt`
	- `neu`
	- Namen vergeben
	- Rechtsklick auf das erstellte Objekt
	- `Bearbeiten`
	- Es sollte sich der Gruppenrichtlinienverwaltungs-Editor öffnen.

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Microsoft Edge`
	- Hier sind nun alle Vorlagen.

- zurück zur `Gruppenrichtlinienverwaltung`
	- Unter `Domain.local` -> `Domäne` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
	- Zum Verknüpfen das gewünschte Objekt auswählen


### Richtlinien in Edge überprüfen
- Die Richtlinien können in Edge unter `chrome://policy` bzw. `edge://policy` eingesehen werden.


-------------------------------------------------------------------------------------------------------------


# Edge Browser deaktivieren/Ausführen von Programmen verbieten
- Die folgende Richtlinie kann das Ausführen von bestimmten Programmen für alle oder nur bestimmte Nutzergruppen verbieten.
- Welche Benutzer von der Richtlinie betroffen sind, hängt davon ab, unter welcher OU (in der Domänen-Struktur) die Richtlinie verknüpft wird.

- Gruppenrichtlinien-Editor öffnen
- Pfad: `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > System`
- `Angegebene Windows-Anwendungen nicht ausführen`
- Wert: 
	- `entsprechender Name des Programms eingeben "name.exe"`
	- z.B. `msedge.exe`
	- Korrekten Namen herausfinden: Auf einem Client anmelden, Rechtsklick auf das Icon des entsprechenden Programms, "Eigenschaften", "Verknüpfung", unter "Ziel" `name.exe` kopieren


-------------------------------------------------------------------------------------------------------------


# Erweiterungen


### Browser-Erweiterungen hinzufügen
- Erweiterungs ID herausfinden:
	- Im Microsoft Erweiterungs-Store die gewünschte Erweiterung aufrufen
	- Die ID aus der Seiten URL (Link) kopieren
	- `?hl` vom Ende der Erweiterung entfernen
	- ID+URL für die GPO muss nach folgendem Schema aussehen: `ErweiterungsID;https://edge.microsoft.com/extensionwebstorebase/v1/crx`

- Beispiele:
	- ErweiterungsID vom [uBlockOrigin Lite](https://ublockorigin.com/de): `cimighlppcgcoapaliogpjjdehbnofhn;https://edge.microsoft.com/extensionwebstorebase/v1/crx`
	- ErweiterungsID vom [Privacy Badger](https://privacybadger.org/): `mkejgcgkdlddbggjhhflekkondicpnop;https://edge.microsoft.com/extensionwebstorebase/v1/crx`
	- ErweiterungsID vom - [Canvas Blocker - Fingerprint Protect](https://microsoftedge.microsoft.com/addons/detail/canvas-blocker-fingerpr/ahiddppepedlomdleppkbljnmkchlmdc?hl=de): `ahiddppepedlomdleppkbljnmkchlmdc;https://edge.microsoft.com/extensionwebstorebase/v1/crx`


- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Edge > Erweiterungen`
- `Steuern, welche Erweiterungen automatisch installiert werden`
- `Anzeigen`
- ID hinzufügen


### Blockieren von Hinzufügen von Erweiterungen aus externen Quellen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Edge > Erweiterungen`
- `Blockiert die Installation externer Erweiterungen` -> Aktiviert


### Blockieren des Entwicklermodus
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Edge > Erweiterungen`
- `Verwenden des Entwicklermodus auf der Erweiterungsseite steuern` -> Aktiviert
- Wert: `Verfügbarkeit des Entwicklermodus auf der Erweiterungsseite steuern`


### Hinzufügen von Erweiterungen durch Nutzer nicht zulassen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Edge > Erweiterungen`
- `Einstellungen für Erweiterungsverwaltung konfigurieren` -> Aktiviert
- Wert (JSON):
	- Blockiert die Installation von Erweiterungen duch Nutzer:
	- Erzwungene Erweiterungen durch die GPO "Erweiterungen hinzufügen" wird durch die Beispiel JSON NICHT beeinträchtigt !
```
{"*":{"installation_mode":"blocked","blocked_install_message":"Die Installation von Erweiterungen ist nicht erlaubt. Bitte wenden Sie sich an den Administrator."}}
```

### Installation bestimmter Erweiterungen zulassen (whitelist) 
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Edge > Erweiterungen`
- `Installation bestimmter Erweiterungen zulassen` -> Aktiviert
- Wert: `entsprechene ID der Erweiterung`
	- [Privacy Badger](https://microsoftedge.microsoft.com/addons/detail/privacy-badger/mkejgcgkdlddbggjhhflekkondicpnop?hl=de): mkejgcgkdlddbggjhhflekkondicpnop
	- [uBlockOrigin Lite](https://microsoftedge.microsoft.com/addons/detail/ublock-origin-lite/cimighlppcgcoapaliogpjjdehbnofhn?hl=de): cimighlppcgcoapaliogpjjdehbnofhn
	- [Dark Reader](https://microsoftedge.microsoft.com/addons/detail/dark-reader/ifoakfbpdcdoeenechcleahebpibofpc?hl=de): ifoakfbpdcdoeenechcleahebpibofpc
	- [Dark Mode](https://microsoftedge.microsoft.com/addons/detail/dark-mode/boldmdfoencgjfblcelefkjfafmpiahm?hl=de): boldmdfoencgjfblcelefkjfafmpiahm
	- [KeePassXC-Browser](https://microsoftedge.microsoft.com/addons/detail/keepassxcbrowser/pdffhmdngciaglkoonimfcmckehcpafo?hl=de): pdffhmdngciaglkoonimfcmckehcpafo
	- [EdgeKeePass](https://microsoftedge.microsoft.com/addons/detail/edgekeepass/jnhjknbfnclancjpknceboifoegiompf?hl=de): jnhjknbfnclancjpknceboifoegiompf
	- [Bitwarden Passwortmanager](https://microsoftedge.microsoft.com/addons/detail/bitwarden-passwortmanager/jbkfoedolllekgbhcbcoahefnbanhhlh?hl=de): jbkfoedolllekgbhcbcoahefnbanhhlh
	- [Startpage - Datenschutz-Suchmaschine](https://microsoftedge.microsoft.com/addons/detail/startpage-%E2%80%94-datenschutzs/jogphcaagccljpbnoddeknjjngefidmm?hl=de): jogphcaagccljpbnoddeknjjngefidmm?
	- [NoScript](https://microsoftedge.microsoft.com/addons/detail/noscript/debdhlbmgmkkfjpcglcbjadbhhekgfjh?hl=de): debdhlbmgmkkfjpcglcbjadbhhekgfjh
	- [Canvas Blocker - Fingerprint Protect](https://microsoftedge.microsoft.com/addons/detail/canvas-blocker-fingerpr/ahiddppepedlomdleppkbljnmkchlmdc?hl=de): ahiddppepedlomdleppkbljnmkchlmdc


### Privaten-Modus deaktivieren (da Erweiterungen standardmäßig nicht im privaten Modus aktiv sind)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Verwaltbarkeit des InPrivate-Modus konfigurieren` -> Aktiviert
- Wert: `InPrivate-Modus deaktiviert`


-------------------------------------------------------------------------------------------------------------


### Überprüfung, ob Edge Standard-PDF-Handler ist deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Inhaltseinstellungen`
- `Entscheiden Sie, ob Benutzer benutzerdefinierte Hintergrundbilder und Texte, Vorschläge, Benachrichtigungen und Tipps für Microsoft-Dienste erhalten können.` -> Deaktiviert


### Überprüfung, ob Edge Standard-PDF-Handler ist deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Inhaltseinstellungen`
- `Benachrichtigungen zum Festlegen von Microsoft Edge als Standard-PDF-Reader zulassen` -> Deaktiviert


### Standardbrowser (verhindern, dass Edge Nutzer bittet ihn als Standardbrowser zu setzen)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Aktiviert Kampangnen für die Standard-Browsereinstellungen` -> Deaktiviert


### Überprüfung, ob Edge Standardbrowser ist deaktivieren
- Richtlinie, zum Blockieren, dass Edge prüft und sich als Standard setzen kann, funktioniert auch unter Win 11 !

- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Microsoft Edge als Standardbrowser festlegen` -> Deaktiviert


### Autostart von Edge Hintergrund Prozessen deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Ausführen von Hintergrund-Apps fortsetzen, nachdem Microsoft Edge geschlossen wurde` -> Deaktiviert


### Google Cast deaktivieren
- Google Cast ist ein proprietäres Protokoll mit welchem Inhalte, wie Musik oder Filme gestreamt werden können.
- Wird in einem Unternehmen in der Regel nicht benötigt und kann für mehr Datenschutzfreundlichkeit deaktiviert werden.


- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Cast`
- `Google Cast aktivieren` -> Deaktiviert
- `Wiedergabesymbol in der Symbolleiste anzeigen` -> Deaktiviert


### Familien-Einstellungen in Edge deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Benutzern die Konfiguration von Family Safty und Kindermodus gestatten` -> Deaktiviert


### Ablagefeature zum ablegen von Nachrichten und Dokumenten in Edge (Nachrichten an sich selbst senden)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Das Ablagefeature in Microsoft Edge aktivieren` -> Deaktiviert


### Daten und Einstellungen eines anderen Browsers bei der ersten Ausführung impotieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Daten und Einstellungen eines anderen Browsers bei der ersten Ausführung automatisch impotieren` -> Aktiviert
- Wert: `Deaktiviert den automatischen Import und überspringt den Importabschnitt der erstmaligen Ausführung`


### RAM-Auslastung durch Edge begrenzen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Dient zum Festlegen des Limits für den Arbeitsspeicher, der von einer einzelnen Microsoft Edge-instanz beansprucht werden kann (in MB)` -> Aktiviert
- Wert: Standardwert:`1024`, für Power-User/mehr als 10 Tabs `2048`


### Empfehlungen und Benachrichtigungen von Edge deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Featureempfehlungen und Browserunterstützungsbenachrichtigungen von Microsoft Edge zulassen` -> Deaktiviert


### Microsoft Rewards deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Microsoft Rewards-Erlebnisse anzeigen` -> Deaktiviert


### Edge Systembenachrichtigungen deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Systembenachrichtigungen zulassen` -> Deaktiviert


### Standardeinstellungen für die Speicherpartitionierung von Drittanbietern
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Inhaltseinstellungen`
- `Standardeinstellungen für die Speicherpartitionierung von Drittanbietern` -> Aktiviert
- Wert: `Deaktivieren Sie die Speicherpartitionierung von Drittanbietern.`


### Außerkraftsetzung der IPv6-Erreichbarkeitsprüfung aktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Netzwerkeinstellungen`
- `Außerkraftsetzung der IPv6-Erreichbarkeitsprüfung aktivieren` -> Aktiviert


### "Eindruck beim ersten Ausführen" und Begrüßungsbildschirm ausblenden (Einführungsbildschirm/Vorschläge)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `"Eindruck beim ersten Ausführen" und Begrüßungsbildschirm ausblenden` -> Deaktiviert


-------------------------------------------------------------------------------------------------------------


# Anmeldeeinstellungen


### Browser-Anmeldeeinstellungen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Browser-Anmeldeeinstellungen` -> Aktiviert
	- Option auswählen, empfohlen: `Browseranmeldung deaktivieren`
- verhindert, dass Microsoft-Konto in MS-Edge genutzt werden kann, inkl. der Kontobezogenen Features, wie Syncronisierung
- die Deaktivierung kann zur Folge haben, dass einige Unterpunkte in den Einstellungen im Browser nicht mehr verfügbar sind und die Seiten leer angezeigt werden


### Cloudsyncronisierung deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Syncronisierung von Daten mit Microsotf-Syncronisierungsdiensten deaktivieren` -> Deaktiviert


### SSO für nicht AAD-konten deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Einmaliges Anmelden auf Arbeits- oder Schulwebsites mit diesem Profil zulassen` -> Deaktiviert


### SSO für persönliche MSA-Konten verhindern
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Einmaliges Anmelden für persönliche Microsoft-Websites mit diesem Profil zulassen` -> Deaktiviert
	- verhindert, dass bei Diensten automatische Anmeldung mit Konten, aus anderen Apps erfolgt 


### SSO für persönliche MSA-Konten verhindern
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Automatische Anmeldung mit einem Active Directory-Domänenjonto konfigurieren, wenn kein Azure AD-Domänenkonto vorhanden ist` -> Aktiviert
- Wert: `Deaktiviert`
	- verhindert, dass Edge automatische Anmeldung mit nicht Azure-AD-Konten (AAD) durchführt


-------------------------------------------------------------------------------------------------------------


# Sicherheits und Datenschutz-Einstellungen


### Sammeln von personenbezogenen Daten durch Microsoft deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Ermöglichen Sie die Personalisierung von Anzeigen, Microsoft Edge, Suche, Nachrichten und anderen Microsoft-Diensten, indem Sie Browserverlauf, Favoriten und Sammlungen, Nutzung und andere Browserdaten an Microsoft senden` -> Deaktiviert


### Verhinderung der Nachverfolgung (Tracking Schutz)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Verbessern Sie den Sicherheitsstatus in Microsoft Edge` -> Aktiviert
- Empfohlen: `Ausgeglichener Modus` für Datenschutz & Sicherheit


### Scareware Blocker deaktivieren (Durchsuchen von Inhalten mit KI)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Einstellungen des Scareware Blockers`
- `Edge Scareware Blocker-Schutz konfigurieren` -> Deaktiviert


### Shopping Assistant deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Shopping in Microsoft Edge aktiviert` -> Deaktiviert


### immer HTTPS verwenden
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Automatisches HTTPS konfigurieren` -> Aktiviert
	- `Alle über HTTP bereitsgestellten Navigationen werden auf HTTPS umgestellt...`


### Senden von Diagnosedaten deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Erforderliche und optionale Diagnosedaten über die Browsernutzung senden` -> Aktiviert
	- Option auswählen, empfohlen: `Aus`


### Benutzerfeedback zulassen deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Benutzerfeedback zulassen` -> Deaktiviert
- verhindert, dass Benutzer nach Feedback gefragt werden


### Drittanbieter-Cookies ablehnen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Cookies von Drittanbieter blockieren` -> Aktiviert
- Cookies von Drittanbietern ablehnen


### verwandte Websitesätze (Microsoft Edge analysiert Surfverhalten -> deaktivieren)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Einstellungen für verwandte Websitesätze`
- `Aktivieren verwandter Websitesätze` -> Deaktiviert


### Passwortmanager deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Kennwort-Manager und -schutz`
- `Speichern von Kennwörtern im Kennwort-Manager ermöglichen` -> Deaktiviert
- `Benutzern das Abrufen eines Vorschlags für sichere Kennwörter gestatten, wenn sie ein online Konto erstellt haben` -> Deaktiviert
- `Ermöglichen von Benachrichtigungen, wenn Kennwörter unsicher sind` -> Deaktiviert


### Deaktivieren des Brieftaschen-Checkout-Features
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Aktivieren des Brieftaschen-Checkout-Features` -> Deaktiviert


### Autofill für Adressen/Zahlungsdaten deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `AutoAusfüllen für Adressen aktivieren` -> Deaktiviert
- `AutoAusfüllen für Zahlungsmittel aktivieren` -> Deaktiviert


### Mitgliedschaften speichern und ausfüllen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Mitgliedschaften speichern und ausfüllen` -> Deaktiviert


### Importieren von Browserdaten aus anderen Browsern in Edge
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Import von Zahlungsinformationen zulassen` -> Deaktiviert
- `Importieren des Browserverlaufs zulassen` -> Deaktiviert
- `Importieren gespeicherter Kennwörter zulassen` -> Deaktiviert
- `Importieren offener Tabs zulassen` -> Deaktiviert
- `Importieren von Cookies zulassen` -> Deaktiviert
- `Importieren von Einstellungen für Startseiten zulassen` -> Deaktiviert
- `Importieren von Erweiterungen zulassen` -> Deaktiviert
- `Importieren von Startseiteneinstellungen zulassen` -> Deaktiviert
- `Importieren von Suchmaschineneinstellungen zulassen` -> Deaktiviert


### Importieren von Browserdaten bei jedem Start von Edge
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Erlauben Sie den Import von Daten aus anderen Browsern bei jedem Start von Microsoft Edge` -> Deaktiviert


### Standardeinstellungen für Popupfenster
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Inhaltseinstellungen`
- `Standardeinstellungen für Popupfenster` -> Aktiviert
- Wert: `Nicht zulassen, dass Websites Popups anzeigen`


### Microsoft Defender SmartScreen konfigurieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > SmartScreen-Einstellungen`
- `Microsoft Defender SmartScreen konfigurieren` -> Aktiviert


### Teilen von Webseiten vom Smartphone zum Desktop
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Hochladen von Dateien von Mobilgeräten in Microsoft Edge-Desktop aktivieren` -> Deaktiviert


-------------------------------------------------------------------------------------------------------------


# KI Einstellungen


### Generative KI
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Generative KI`
- `Einstellungen für das lokale GenAI-Basismodell` -> Aktiviert
- `Modell nicht herunterladen` auswählen


### KI-generierten Designs über DALL-E deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Aktiviert die Generierung von DALL-E Designes` -> Deaktiviert


### Durch maschinelles Lernen unterstützte AutoAusfüllen-Vorschläge
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Durch maschinelles Lernen unterstützte AutoAusfüllen-Vorschläge` -> Deaktiviert


### Spracherkennung konfigurieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Spracherkennung konfigurieren` -> Deaktiviert


-------------------------------------------------------------------------------------------------------------


# Darstellungs- / Starteinstellungen


### Edge Arbeitsbereiche deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Einstellungen für Edge-Arbeitsbereiche`
- `Arbeitsbereiche aktivieren` -> Deaktiviert
- `Konfigurieren von Navigationseistellungen pro URLs in MS-Esge Arbeitsbereichen`  -> Deaktiviert


### Startseite Vorschläge & Hintergrundbilder deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Start, Startseite und neue Tabs`
- `Hintergrundtypen konfigurieren, die für das Seitenlayout des neuen Tabs zulässig sind` -> Aktiviert `Alle Hintergrundbildtypen deaktivieren`
- `Zulassen von Microsoft-Inhalten auf der neuen Registerkartenseite` -> Deaktiviert


### Angeheftete Links auf der Startseite hinzufügen (max. 3 Kachel-Elemente können über diese GPO hinzugefügt werden)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Start, Startseite und neue Tabs`
- Angepinnte Elemente hinzufügen: `Schnelllinks für neue Tabs festlegen` -> Aktiviert
- Folgendes Einfügen (Beispiel Elemente):
```
[{"url":"https://www.Beispiel.com/","title":"Beispiel","pinned":true},{"url":"https://www.Beispiel.com/","title":"Beispiel","pinned":true}]
```
oder
```
[{"url":"https://www.ecosia.org","title":"Ecosia","pinned":true},{"url":"https://www.startpage.com","title":"Startpage","pinned":true},{"url":"https://www.google.com","title":"Google","pinned":true}]
```


### Quicklinks-Kachel-Elemente deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Start, Startseite und neue Tabs`
- `Quicklinks auf der Seite "Neue Registerkarte" zulassen` -> Deaktiviert


### App-Launcher deaktivieren (Schnell-Links zu MS-365 Produkten entfernen)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Start, Startseite und neue Tabs`
- `App Launcher auf Microsoft Edge Seite "Neue Registerkarte" ausblenden` -> Deaktiviert


### Assistent für das Anheften an die Taskleiste deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Assistent für das Anheften an die Taskleiste zulassen` -> Deaktiviert
- verhindert, dass Edge vorschlägt sich an die Taskleiste anzuheften


### Deaktivieren des Microsoft-Edge-Minimenü
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Aktiviert das Microsoft Edge Minimenü` -> Deaktiviert


### URL zur "neue Tabseite" konfigurieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Start, Startseite und neue Tabs`
- `URL für die neue Tabseite konfigurieren` -> Aktiviert
- Wert: Die entsprechende URL zur gewünschten Webseite


-------------------------------------------------------------------------------------------------------------


# Suche

### Trendvorschläge in Adressleiste deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Microsoft Bing-Trendvorschläge in der Adresseleiste aktivieren` -> Deaktiviert


### Suchvorschläge deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Suchvorschläge aktivieren` -> Deaktiviert


### Suchmaschine in MS-Edge anpassen 
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Suchmaschienen verwalten` -> Aktiviert
- Wert:

[Startpage](https://www.startpage.com/):
```
[{"encoding":"UTF-8","is_default":true,"keyword":"startpage.com","name":"Startpage","search_url":"https://www.startpage.com/do/dsearch?query={searchTerms}","suggest_url":"https://www.startpage.com/do/suggest?q={searchTerms}"}]
```

[Qwant](https://www.qwant.com/):
```
[{"encoding":"UTF-8","is_default":true,"keyword":"qwant.com","name":"Qwant","search_url":"https://www.qwant.com/?q={searchTerms}","suggest_url":"https://api.qwant.com/api/suggest/?q={searchTerms}"}]
```

[DuckDuckGo](https://duckduckgo.com/):
```
[{"encoding":"UTF-8","is_default":true,"keyword":"duckduckgo.com","name":"DuckDuckGo","search_url":"https://duckduckgo.com/?q={searchTerms}","suggest_url":"https://duckduckgo.com/ac/?q={searchTerms}"}]
```

[Ecosia](https://www.ecosia.org/):
```
[{"encoding":"UTF-8","is_default":true,"keyword":"ecosia.org","name":"Ecosia","search_url":"https://www.ecosia.org/search?q={searchTerms}","suggest_url":"https://ac.ecosia.org/autocomplete?q={searchTerms}"}]
```


### Top-Websites personalisieren in Seitenleiste anpassen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Meine Top-Websites personalisieren in Seitenleiste anpassen standardmäßig aktiviert` -> Deaktiviert


### Suchleiste deaktivieren (Verknüpfung, ähnlich wie ein Widget auf dem Desktop)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Aktivieren der Suchleiste` -> Deaktiviert


### Zusätzliches Suchfeld im Browser aktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Zusätzliches Suchfeld im Browser aktivieren` -> Deaktiviert


### Browserdaten aus MS-Edge in der Suchlesite in der Taskleiste
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Windows die Suche nach lokalen Microsoft Edge Browserdaten ermöglichen` -> Deaktiviert


-------------------------------------------------------------------------------------------------------------


# Verwaltbarkeit


### Die Verwaltung mobiler Apps ist aktiviert
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Verwaltbarkeit`
- `Die Verwaltung mobiler Apps ist aktiviert` -> Deaktiviert


### Feedback zu Microsotf Edge-Verwaltungserweiterungen aktiviert
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Verwaltbarkeit`
- `Feedback zu Microsotf Edge-Verwaltungserweiterungen aktiviert` -> Deaktiviert


### Microsoft Edge-Verwaltung aktiviert (MS Edge cloudbasierten Verwaltungsoberfläche im MS 365 Admin Center)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Verwaltbarkeit`
- `Microsoft Edge-Verwaltung aktiviert` -> Deaktiviert


### Microsoft Edge-Verwaltungsregistrierungstoken (MS Edge cloudbasierten Verwaltungsoberfläche im MS 365 Admin Center)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Verwaltbarkeit`
- `Microsoft Edge-Verwaltungsregistrierungstoken` -> Deaktiviert


### Zulassen, dass Benutzerrichtlinen des cloudbasierten Microsoft Edge-Verwaltungsdienstes lokale Benutzerrichtlinien außer Kraft setzen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Verwaltbarkeit`
- `Zulassen, dass Benutzerrichtlinen des cloudbasierten Microsoft Edge-Verwaltungsdienstes lokale Benutzerrichtlinien außer Kraft setzen` -> Deaktiviert


-------------------------------------------------------------------------------------------------------------
