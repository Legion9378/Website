# Fiction-Modul

## Ziel

Das Fiction-Modul ist ein eigenstaendiges Website-Modul fuer Original-Stories und Fanfiction. Es ist vom Blog-Modul, von KI-Workflows und vom KI-Netzwerk getrennt.

Das Modul soll klassisch auf Webhosting laufen:

- HTML
- PHP
- MySQL/MariaDB
- CSS
- gezieltes JavaScript/HTMX nur dort, wo es fuer Bedienung und Fragmente sinnvoll ist

Kein Docker, keine Container und keine lokale Konvertierung durch User.

## Abgrenzung

### Gehoert zum Fiction-Modul

- Original-Stories
- Fanfiction
- Autoren-Zugriffe
- Online-Lesen
- Reviews und optional Kommentare
- Story-Downloads
- Admin-Funktionen fuer Stories, User, Reviews und Exporte

### Gehoert nicht zum Fiction-Modul

- Blogposts
- KI-Blogpost-Webhooks
- KI-Zugriff auf User-Stories
- KI-gestuetzte Uebersetzung von User-Stories
- allgemeine Website-Module wie Paywall, Shop oder Landingpages

Blogposts sind ein eigenes Modul. Autoren kontrollieren Stories und Uebersetzungen selbst.

## Rollen und Funktionen

### Autoren

- Story erstellen
- Kapitel hinzufuegen und bearbeiten
- Metadaten pflegen:
  - Titel
  - Beschreibung
  - Autor
  - Tags
  - Warnungen
  - Cover
- Sichtbarkeit steuern:
  - Draft
  - Published
- eigene Exporte anstossen oder regenerieren

### Leser

- Stories online lesen
- Kapitelansicht und Volltextmodus nutzen
- Next/Previous-Navigation
- Reviews schreiben
- optionale moderierbare Kommentare nutzen
- verfuegbare Downloadformate direkt herunterladen

### Administratoren

- Benutzer verwalten
- Rollen verwalten
- Stories/Kapitel pruefen, sperren, freigeben, loeschen
- Reviews/Kommentare moderieren
- Statistiken und Logs einsehen
- Export-Cache pruefen, loeschen oder neu generieren

## Datenmodell Kandidat

### `users`

- `id`
- `username`
- `email`
- `password_hash`
- `role` (`author`, `admin`, `reader`)
- `created_at`

### `stories`

- `id`
- `title`
- `description`
- `cover_path`
- `author_id`
- `status` (`draft`, `published`)
- `created_at`
- `updated_at`
- `tags`
- `warnings`

### `chapters`

- `id`
- `story_id`
- `chapter_number`
- `title`
- `content`
- `created_at`
- `updated_at`

### `reviews`

- `id`
- `story_id`
- `user_id`
- `rating`
- `comment`
- `created_at`
- `status` (`pending`, `published`, `hidden`)

### `exports`

Optionaler Cache fuer generierte Dateien:

- `id`
- `story_id`
- `format`
- `file_path`
- `created_at`
- `expires_at` oder `source_hash`

## Export-Regel

Alle Downloadformate muessen fuer User serverseitig generierbar und direkt im Browser herunterladbar sein.

Unterstuetzte Zielformate:

- HTML
- TXT
- PDF
- EPUB
- DOCX
- RTF
- MOBI

Umsetzungsoptionen:

- HTML/TXT: direkt aus Datenbankinhalt erzeugen
- PDF: DomPDF oder vergleichbare PHP-Loesung
- EPUB: PHPePub oder vergleichbare PHP-Bibliothek
- DOCX/RTF: PHPWord oder vergleichbare PHP-Bibliothek
- MOBI: serverseitig aus EPUB erzeugen, z. B. ueber Kindlegen oder Calibre/ebook-convert, falls der Hoster CLI-Ausfuehrung erlaubt

Wichtig: MOBI darf nicht als lokale Konvertierung auf Bjoerns Rechner oder beim User geplant werden. Wenn MOBI angeboten wird, muss es serverseitig als Download bereitstehen.

## Rechte und Sicherheit

- Autoren duerfen eigene Stories und Kapitel bearbeiten.
- Admins duerfen alle Stories, Reviews, Benutzer und Exporte verwalten.
- Leser duerfen oeffentliche Stories lesen und Reviews schreiben.
- Downloads duerfen nur fuer veroeffentlichte Stories ausgeliefert werden.
- Drafts und private Inhalte duerfen nicht ueber Export-Endpunkte erreichbar sein.
- Export-Endpunkte brauchen Rechtepruefung und Rate-/Cache-Strategie.
- Uploads wie Cover brauchen Dateityp-, Groessen- und Pfadpruefung.

## Frontend-Regeln

- Storyseite: Cover, Metadaten, Tags, Warnungen, Kapiteluebersicht, Downloadbuttons.
- Lesemodus: Kapitelweise und optional Volltext.
- Autorenseite: Story-/Kapitel-CRUD, Metadaten, Cover-Upload, Status.
- Adminseite: Benutzer, Stories, Reviews, Exporte, Logs.
- HTMX darf fuer Formulare, Listen, Moderation, Review-Updates und Exportstatus genutzt werden.
- Keine schwere SPA-Logik, solange serverseitige HTML/PHP/HTMX-Komponenten reichen.

## Naechste Coding-Schritte

1. Datenmodell finalisieren.
2. Rechte-/Rollenmodell pruefen.
3. Minimalen Story-/Chapter-CRUD fuer Autoren bauen.
4. Oeffentliche Story-/Kapitelansicht bauen.
5. Review-/Moderationsmodell implementieren.
6. Exportpipeline zuerst fuer HTML/TXT, danach PDF/EPUB/DOCX/RTF, zuletzt MOBI pruefen.
7. Export-Cache und Regenerierungslogik ergaenzen.

## Quelle

Ausgewertet aus Chat-History:

`chatgpt-funktionsvergleich-bookstack-versionen-2026-05-07T01-16-51-953Z.md`
