# CMS-Sprachen und Translation-Queue

Stand: 2026-07-06
Status: Planungsregel / spaeter praktisch testen
Quelle: Chat-History `chatgpt-webgpu-und-ki-nutzung-2026-05-07T02-25-06-426Z.md`

## Korrigierte Entscheidung

Der aktive Startumfang fuer Website-/CMS-Content ist auf **Deutsch und Englisch** reduziert.

Gruende:

- Weniger Arbeit fuer die KI beim Erstellen und Pflegen von Content.
- Bjoern kann Deutsch und Englisch selbst sprachlich kontrollieren.
- Fuer Franzoesisch, Spanisch, Italienisch, Niederlaendisch usw. fehlt Bjoern die persoenliche Sprachkontrolle.
- Andere Sprachen werden nicht als automatische CMS-/KI-Erstellungsdefaults gefuehrt.
- Uebersetzungen in weitere Sprachen sollen spaeter anders und gezielt geplant werden, nicht ueber eine pauschale 5-Sprachen-Queue.

## Regeln fuer den Start

- Primaere Content-Sprachen: `de`, `en`.
- Kein automatischer 5-Sprachen-Default.
- Keine zusaetzlichen Sprachen nur wegen geografischer Reichweite.
- Neue Sprachversionen nur mit eigenem Konzept fuer Qualitaetskontrolle, Review und Kosten/Nutzen.

## Queue-/Lastprinzip

Auch bei nur zwei Sprachen gilt:

- Uebersetzung/Sprachfassung nicht synchron im Seitenrequest erzeugen.
- Content-Erstellung und Sprachfassung als Hintergrundjob oder Werkbank-Schritt planen.
- Webserver darf nicht durch Sprachgenerierung blockieren.
- Worker-Zahl, DB-Writes, Cache und Logging spaeter real testen.

## WebGPU-Einordnung

WebGPU ist fuer diese CMS-Sprachplanung keine Startvoraussetzung.

Das Problem ist nicht Browser-GPU, sondern Content-/CMS-Architektur:

- klare Quellsprache;
- kontrollierte Sprachfassung;
- Review durch Bjoern;
- spaetere gezielte Uebersetzungsstrategie.

## Nicht uebernehmen

- Der alte 5-Sprachen-Default `DE/EN/FR/ES/IT` ist verworfen.
- Niederlaendisch wird nicht automatisch als naechste Sprache eingeplant.
- Alte Pi-4-Beitragszahlen sind nur grobe Plausibilitaet, keine Kapazitaetsgarantie.
- Keine WebGPU-/Browsermodell-Architektur aus dieser Quelle ableiten.
