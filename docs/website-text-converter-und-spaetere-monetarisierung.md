# Website Text-Converter und spaetere Monetarisierung

Stand: 2026-07-08
Status: Planungsnotiz
Quelle: Chat-History `chatgpt-lightning-node-anforderungen-2026-05-07T08-34-35-456Z.md`

## Entscheidung

Aus der Mini-Tool-Liste wird vorerst nur der Text-Converter uebernommen.

Nicht uebernommen:

- URL-Kuerzer;
- Einheitenumrechner;
- Zeitzonenrechner;
- Base64-Konverter;
- Passwortgenerator/Passwortstaerke-Pruefer;
- JSON-Formatter/-Validator;
- Whois/IP-Info;
- Markdown-Vorschau;
- Bildgroessenberechner;
- sonstige generische Mini-Tools.

## Text-Converter Scope

Der Text-Converter ist ein ressourcenarmes Website-Tool fuer einfache Textumwandlungen und Copy-Paste-Aufraeumarbeiten.

Moegliche Funktionen:

- Gross-/Kleinschreibung umwandeln;
- Sonderzeichen, doppelte Leerzeichen oder Zeilenumbrueche bereinigen;
- Unicode-/ASCII-nahe Anzeigen oder einfache Konvertierungen;
- einfache, harmlose Formatbereinigung fuer kopierte Texte.

Technische Zielrichtung:

- bevorzugt Frontend-only mit JavaScript;
- keine Benutzerkontenpflicht;
- keine serverseitige Speicherung eingegebener Texte;
- keine sensiblen Eingaben erfragen;
- spaeter in die modulare Website integrierbar.

## Werbung / Monetarisierung

Werbung wird nur als spaetere Option notiert, nicht als aktuelle Umsetzung.

Regel:

- Erst nutzbares Tool und saubere UX;
- danach Monetarisierung pruefen;
- Werbung darf Funktion und Vertrauen nicht zerstoeren.

## Punkte / Satoshi / Lightning

Das Punkte-/Satoshi-/Lightning-Thema wird ganz hinten geparkt.

Aktueller Status:

- keine Lightning-Node-Installation aus dieser Quelle;
- keine Satoshi-Auszahlung als aktuelles Website-Feature;
- wenn spaeter relevant: monatliche Abrechnung/Umrechnung als Kontrollmechanismus pruefen, nicht Echtzeit-Auszahlung als Default.

## Nicht aus dieser Quelle uebernehmen

- URL-Kuerzer mit Werbe-Zwischenseite;
- vollstaendige Mini-Tool-Sammlung;
- Lightning Node als aktuelle Infrastrukturentscheidung;
- Mac Mini/Raspberry Pi als Hosting-Entscheidung;
- DOCX-Export aus dem Chat.
