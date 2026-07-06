# Modulares Website-Framework und App-Rebuild

Stand: 2026-07-06
Status: Planungsregel / Umsetzung nur nach Review
Quelle: Chat-History `chatgpt-yunohost-auf-raspberry-pi-4-2026-05-07T01-14-16-829Z.md`

## Kurzthese

Website-Funktionalitaet soll langfristig als eigenes modulares Framework unter einer Hauptdomain laufen, nicht als Sammlung separater YunoHost-Apps mit eigener Subdomain, Authentifizierung und Datenlogik.

YunoHost kann Hosting-/Testumgebung sein, ist aber keine Kernabhaengigkeit der eigentlichen Website-Architektur.

## Architekturprinzipien

- Module laufen innerhalb der Hauptseite, z. B. als `/module/wiki`, `/module/blog`, `/module/audio` oder spaeter festgelegte Pfade.
- Keine Subdomain-Zersplitterung fuer jedes Modul.
- Zentrale Benutzerlogik statt separater App-Accounts.
- Zentrale Auth-/Session-/Rollenlogik.
- Zentrale Punkte-/Wallet-/Aktionslogik, falls dieses Feature aktiv bleibt.
- Einheitliches UI/Theme und gemeinsame Navigation.
- Gemeinsame DB-/API-Schicht statt isolierter App-Dateninseln.

## Umgang mit bestehenden Apps

Bestehende Apps wie YunoHost-Apps, Bookstack, Wiki-, Blog- oder Audio-Tools duerfen als Referenz fuer Funktionsumfang, Datenmodell und UX analysiert werden.

Nicht erlaubt als Standard:

- fremden Code 1:1 kopieren;
- Lizenzgrenzen ignorieren;
- App-Installationsskripte blind uebernehmen;
- SSOwat-/YunoHost-spezifische Annahmen in die eigene Kernarchitektur ziehen.

Stattdessen:

1. Quellprojekt/Feature als Analyseobjekt erfassen.
2. `analysis_report.md` erstellen:
   - Framework/Sprache;
   - zentrale Datenmodelle;
   - Routing/API;
   - Auth-/Rechtekonzept;
   - wichtigste UX-Flows;
   - Abhaengigkeiten;
   - Lizenzhinweise.
3. Review-Gate: entscheiden, welche Funktionen wirklich gebraucht werden.
4. Eigene Implementierung im Website-Framework planen.
5. Testen, ob das Modul portabel laeuft.

## Portabilitaet

Ziel ist ein transportierbares Website-System, das nicht fest an YunoHost gebunden ist.

Zielplattformen koennen spaeter sein:

- YunoHost als bequeme Hosting-/Testumgebung;
- normaler Webspace, soweit Runtime/DB passen;
- eigener Root-/VServer;
- eigener Nginx-/Caddy-Stack.

Portabilitaet ist erst belegt, wenn Deployment, Datenbank, Pfade, Cronjobs/Worker, Uploads, Caching und Rechte auf der Zielplattform getestet wurden. Die alte Annahme "nur DB/API-Endpunkte anpassen" ist zu optimistisch und gilt nicht als Nachweis.

## Nicht als aktueller Scope uebernehmen

- YunoHost `MyApp` ist Option, keine Pflicht.
- Kubernetes ist kein Ziel aus dieser Quelle.
- NFT-/Mini-Game-/Story-KI-Beispiele sind keine automatische Scope-Freigabe.
- KI-Reimplementation ist nicht autonom: Analyse, Lizenzpruefung, Review und Tests bleiben Pflicht.
