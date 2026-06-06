# Frontend-Architektur

## Ziel

Diese Website basiert weiterhin auf dem WordPress-Basecode. WordPress bleibt die stabile Grundlage fuer Bootstrap, Datenmodell, Admin-Bereich, Benutzerverwaltung, Inhalte, Routing-nahe Funktionen und kompatible Erweiterungspunkte.

Das oeffentliche Frontend wird jedoch als eigene lokale Schicht neu aufgebaut. Die bevorzugten Bausteine sind HTML, PHP, HTMX und gezieltes JavaScript. Schwere Frontend-Frameworks und deren Altlasten sollen vermieden werden.

## Grundregeln

1. WordPress-Core bleibt updatefaehig und wird moeglichst nicht direkt veraendert.
2. Eigener Code liegt in lokalen Themes, Plugins, Modulen oder klar getrennten Frontend-Dateien.
3. Bestehende WordPress-Vorlagen duerfen als fachliche und strukturelle Orientierung gelesen werden.
4. Es wird kein Code aus bestehenden Vorlagen kopiert, wenn daraus eigene lokale Bausteine entstehen.
5. Neue Plugins, Module, Erweiterungen und Designs muessen zum neuen HTML/PHP/HTMX/JavaScript-Frontend passen.
6. Jede Frontend-Entscheidung soll die Abhaengigkeit von schwergewichtigen Framework-Strukturen reduzieren.

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
- bestehende WordPress-Muster nur als Referenz nutzen

## Arbeitsregel

Bei jeder neuen Anpassung zuerst pruefen:

1. Kann die Aenderung ohne Core-Eingriff umgesetzt werden?
2. Gehoert sie in ein Theme, ein Plugin, ein Modul oder in eine Frontend-Komponente?
3. Passt sie zum HTML/PHP/HTMX/JavaScript-Frontend?
4. Wurde bestehender WordPress-Code nur verstanden, aber nicht kopiert?

Nur wenn diese Fragen sauber beantwortet sind, soll Code ergaenzt werden.
