# Frontend-Architektur

## Ziel

Diese Website basiert weiterhin auf dem WordPress-Basecode. WordPress bleibt die stabile Grundlage fuer Bootstrap, Datenmodell, Admin-Bereich, Benutzerverwaltung, Inhalte, Routing-nahe Funktionen und kompatible Erweiterungspunkte.

Das oeffentliche Frontend wird jedoch als eigene lokale Schicht neu aufgebaut. Die bevorzugten Bausteine sind HTML, PHP, HTMX und gezieltes JavaScript. Schwere Frontend-Frameworks und deren Altlasten sollen vermieden werden.

## Ursprung der Entscheidung

Der Ausloeser fuer diese Richtung war der Artikel `HTMX vs React: We Built the Same Feature Twice` und eine anschliessende Besprechung mit ChatGPT.

Die uebernommene Idee ist nicht `React ist schlecht`, sondern: Die Architektur soll proportional zur Anforderung bleiben. Kleine Interaktionen, Formulare, Frontend-Fragmente und klassische Website-Funktionen sollen nicht automatisch als schwere clientseitige State-Maschine umgesetzt werden.

Fuer diese Website bedeutet das:

- WordPress bleibt die stabile Backend- und Admin-Basis.
- Das oeffentliche Frontend darf als eigene Schicht entstehen.
- HTML, PHP, HTMX und gezieltes JavaScript werden zuerst geprueft.
- React oder andere Frameworks bleiben nur dann Kandidaten, wenn echte Client-Komplexitaet entsteht.

## Grundregeln

1. WordPress-Core bleibt updatefaehig und wird moeglichst nicht direkt veraendert.
2. Eigener Code liegt in lokalen Themes, Plugins, Modulen oder klar getrennten Frontend-Dateien.
3. Bestehende WordPress-Vorlagen duerfen als fachliche und strukturelle Orientierung gelesen werden.
4. Es wird kein Code aus bestehenden Vorlagen kopiert, wenn daraus eigene lokale Bausteine entstehen.
5. Neue Plugins, Module, Erweiterungen und Designs muessen zum neuen HTML/PHP/HTMX/JavaScript-Frontend passen.
6. Jede Frontend-Entscheidung soll die Abhaengigkeit von schwergewichtigen Framework-Strukturen reduzieren.
7. KI-Hintergrundsteuerung fuer User-Interaktion oder aktive Seitenlogik ist kein Ziel dieser Website-Architektur.

## Geplante Schichten

### WordPress-Basecode

Der Basecode liefert die Plattformfunktionen. Dazu gehoeren insbesondere:

- Core-Bootstrap
- Admin-Bereich
- Datenbankmodell
- Benutzer- und Rechteverwaltung
- Content-Verwaltung
- Plugin- und Theme-Lifecycle
- bestehende WordPress-APIs

Direkte Core-Aenderungen sind nur eine Notloesung. Wenn eine Anpassung ueber Theme, Plugin, Hook, Filter oder eigene Module moeglich ist, hat diese Variante Vorrang.

### Neues Frontend

Das neue Frontend wird aus kleinen, nachvollziehbaren Bausteinen aufgebaut:

- PHP fuer serverseitige Templates und WordPress-Anbindung
- HTML als primaere Ausgabestruktur
- HTMX fuer gezielte Interaktion ohne grosse SPA-Schicht
- JavaScript fuer Verhalten, das nicht sinnvoll mit HTML, PHP oder HTMX geloest wird
- CSS als lokale, kontrollierte Gestaltungsschicht

Das Frontend soll die WordPress-Daten und APIs nutzen, aber nicht automatisch die klassische WordPress-Theme- oder Block-Frontend-Logik uebernehmen.

### Lokale Erweiterungen

Plugins, Module, Erweiterungen und Designs werden lokal erstellt. Sie sollen:

- klar benannt und abgegrenzt sein
- keine unnoetigen externen Abhaengigkeiten einfuehren
- updatefaehig neben dem WordPress-Core existieren
- die neue Frontend-Schicht respektieren
- bestehende WordPress-Muster, Plugins und Module nur als Referenz nutzen
- eigenstaendig programmiert werden und keinen Code aus fremden Plugins oder Modulen uebernehmen



## Auth / User-Management (Kandidat)

AlsAuth-Baustein für die Website wird das **Rotorcipher-Pepper-Design** geprüft (siehe `kb/password-rotor-pepper-pattern.md`):

- Eigenes Passwort-Design: Rotorcipher (100 Rotoren + 4 Reflektoren) als fixer Pepper vor Argon2id
- Pure PHP 7.4+/8.x, Webhosting-kompatibel, keine externen Dependencies
- Ersetzt `wp_hash_password` / `wp_check_password` via Plugin oder `mu-plugins`
- Separate User-Encryption (25 Rotoren) für PII (E-Mail, Adresse, etc.) mit Canvas/SVG-Rendering
- Admin-Encryption (50 Rotoren) für System-Secrets, API-Keys, Config

### 🚫 BLOCKER (müssen gelöst sein vor Integration)

| # | Blocker | Beschreibung | Priorität |
|---|---|---|---|
| **B1** | **KDF/HMAC-Ableitung für Steps/Dirs** | Unsicherer `srand`-Platzhalter in `rotor_preprocess_password()` → **HMAC/KDF von Master-Key** nötig | **KRITISCH** |
| **B2** | **HMAC über Metadaten** | User/Admin-Encryption Metadaten ohne Integritätsschutz → **Manipulation möglich** | **KRITISCH** |
| **B3** | **Key-Rotation / Migration** | Pepper-Wechsel = **alle Hashes ungültig** → **Migration-Pfad fehlt** | **HOCH** |
| **B4** | **Security-Audit** | Eigenes Krypto → **externe Review nötig** (Side-Channel, Timing, Alphabet) | **KRITISCH** |
| **B5** | **WP-Plugin / Micro-Service Integration** | `wp_hash_password` Override via `mu-plugins` oder Micro-Service → **Entscheidung & Implementation** | **HOCH** |

Status: **Analyse-Kandidat** — **5 BLOCKER offen**, erst nach **ALLE gelöst** + Hardening + Tests setzen.

## Arbeitsregel

Bei jeder neuen Anpassung zuerst pruefen:

1. Kann die Aenderung ohne Core-Eingriff umgesetzt werden?
2. Gehoert sie in ein Theme, ein Plugin, ein Modul oder in eine Frontend-Komponente?
3. Passt sie zum HTML/PHP/HTMX/JavaScript-Frontend?
4. Wurde bestehender WordPress-Code nur verstanden, aber nicht kopiert?

Nur wenn diese Fragen sauber beantwortet sind, soll Code ergaenzt werden.
