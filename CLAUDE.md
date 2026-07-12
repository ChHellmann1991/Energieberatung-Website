# CLAUDE.md

## Projektüberblick

Website für Ingenieurbüro Hellmann (Energieberatung, Böblingen) — live unter https://www.energie-hellmann.de.

**Für Business-Details (Leistungen, Zielgruppe, USPs, SEO-Fokus) siehe [docs/business-context.md](docs/business-context.md).**

## Technischer Stack

- **Rein statisch:** handgeschriebenes HTML/CSS/JS. Kein Framework, kein Build-Schritt, kein npm, keine Abhängigkeiten — das soll so bleiben.
- **Deployment:** GitHub Pages, Branch `main`, Root-Verzeichnis. Push auf `main` = sofort live. Kein CI/CD-Workflow, keine Actions (gewollt). Domain via [CNAME](CNAME), DNS bei IONOS (siehe [README.md](README.md)).
- **Lokal testen:** `python -m http.server 8000`

### Ordnerstruktur

```
*.html              Seiten flach im Root (index, leistungen, partner, ueber-mich, kontakt, impressum, datenschutz)
css/style.css       Einziges Stylesheet (Designsystem mit CSS-Variablen)
js/main.js          Einziges Script (Mobile-Menü, Scroll-Animationen, Formular-Feedback)
fonts/              Inter lokal gehostet (datenschutzkonform — kein Google Fonts!)
images/             Bilder und Logos
CNAME               Custom Domain für GitHub Pages
robots.txt, sitemap.xml, google*.html   SEO / Search Console
```

## Konventionen

- **Dateinamen:** Seiten kleingeschrieben, deutsch, flach im Root (`leistungen.html`), Umlaute umschrieben (`ueber-mich.html`).
- **Kein Templating:** Header/Nav/Footer sind auf jeder Seite dupliziert. Bei Änderungen daran **alle 7 Seiten** konsistent anpassen.
- **CSS:** BEM-artige Klassennamen (`hero__title`, `nav__link--active`, `btn btn--primary`). Farben/Abstände nur über CSS-Variablen aus `:root` in [css/style.css](css/style.css). Variablennamen sind lowercase (`--color-primary`, nicht `--Color-primary`).
- **JS:** Vanilla JS, alles in [js/main.js](js/main.js), keine Libraries.
- **Neue Seite anlegen:** individuellen `<title>`, `meta description`, `rel="canonical"` und OG-Tags setzen; Nav + Footer auf **allen** Seiten ergänzen; in [sitemap.xml](sitemap.xml) eintragen.
- **Bilder:** immer mit sinnvollem `alt`-Text (Bestand ist vollständig — so halten).
- **Strukturierte Daten:** Schema.org `ProfessionalService` auf index.html, `FAQPage` auf leistungen.html — bei Adress-/Leistungs-/FAQ-Änderungen mitpflegen.
- **Datenschutz-Prinzip:** Fonts lokal, Analytics nur GoatCounter, Formular via Web3Forms. Keine Google-Fonts-, CDN- oder Tracking-Einbindungen, die Daten an Dritte senden.

## Ton & Sprache

- Deutsch, Sie-Form, seriös und kompetent, kein Marketing-Sprech.
- Fachbegriffe korrekt und konsistent: iSFP, Heizlastberechnung nach DIN EN 12831 (raumweise), hydraulischer Abgleich nach Verfahren B, Lüftungskonzept nach DIN 1946-6, Bestätigung zum Antrag (BzA), BEG, Energieeffizienz-Experte (EEE).
- Preishinweis einheitlich: „Alle Preise als Kleinunternehmer nach § 19 UStG – es fällt keine Umsatzsteuer an."

## Bekannte Besonderheiten / Stolperfallen

- **Deployment ist rein manuell** (git push). Es gibt keine Tests, keinen Linter, keine Link-Prüfung — nichts läuft automatisch.
- **FAQ doppelt gepflegt:** Die FAQs in [leistungen.html](leistungen.html) existieren zweimal — als JSON-LD (`FAQPage`) im `<head>` und als sichtbare Sektion. Beide müssen synchron bleiben.
- **Performance:** Bilder unoptimiert (`hero.png` ~940 KB, `logo.png` ~471 KB, `profil.png` ~303 KB), kein `loading="lazy"`, keine `width`/`height`-Attribute, kein WebP. Größter Optimierungshebel.
- **Barrierefreiheit:** solide Basis, aber kein Skip-Link, `aria-expanded` fehlt am Mobile-Menü-Button, Emoji-Icons nicht als dekorativ markiert.
- **Bug:** [index.html](index.html) enthält einmal `var(--Color-primary)` (großes C) — Variable greift nicht.
- Viele Inline-Styles in den HTML-Dateien; bei größeren Umbauten schrittweise in [css/style.css](css/style.css) überführen.
- Das Repo liegt in einem OneDrive-Ordner — bei Sync-Konflikten können Duplikat-Dateien entstehen.

## Was ich NICHT möchte

- **Kein `git push` / Deploy ohne explizite Freigabe.** Commits lokal sind ok, wenn beauftragt.
- **Preise & Konditionen** (Preisboxen und Preistabelle in [leistungen.html](leistungen.html)) nur nach expliziter Freigabe ändern.
- Keine Frameworks, Bundler oder externen Abhängigkeiten einführen.
- Konkrete Förderdetails (Bonushöhen, Fristen, Programmänderungen wie z. B. eine KfW-458-Reform) gehören **nicht** in CLAUDE.md oder docs/business-context.md — das ist Content und wird direkt in den Seiteninhalten gepflegt.
