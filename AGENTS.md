# AGENTS.md

## Projektüberblick

Website für Ingenieurbüro Hellmann (Energieberatung, Böblingen) — live unter https://www.energie-hellmann.de.

**Für Business-Details (Leistungen, Zielgruppe, USPs, SEO-Fokus) siehe [docs/business-context.md](docs/business-context.md).**

## Technischer Stack

- **Rein statisch:** handgeschriebenes HTML/CSS/JS. Kein Framework, kein Build-Schritt, kein npm, keine Abhängigkeiten — das soll so bleiben.
- **Deployment:** GitHub Pages, Branch `main`, Root-Verzeichnis. Push auf `main` = sofort live. Kein CI/CD-Workflow, keine Actions (gewollt). Domain via [CNAME](CNAME), DNS bei IONOS (siehe [README.md](README.md)).
- **Lokal testen:** `python -m http.server 8000`

### Ordnerstruktur

```
*.html              Seiten flach im Root (index, leistungen, referenzen, partner, ueber-mich, kontakt,
                    energieausweis, photovoltaik, anfrage, impressum, datenschutz + 4 Ortsseiten:
                    energieberatung-sindelfingen/-herrenberg/-leonberg/-holzgerlingen)
css/style.css       Einziges Stylesheet (Designsystem mit CSS-Variablen, CRLF-Zeilenenden)
js/main.js          Einziges Script (Mobile-Menü, Scroll-Animationen, Formular-Feedback)
fonts/              Inter lokal gehostet (datenschutzkonform — kein Google Fonts!)
images/             Bilder und Logos (nur eingebundene Web-Dateien — keine EPS, PDFs oder Belege!)
docs/               Interne Doku (Business-Kontext, SEO-Plan, Änderungsspezifikationen)
_config.yml         Jekyll-Konfiguration für GitHub Pages: schließt AGENTS.md, README.md und docs/ vom Deploy aus
CNAME               Custom Domain für GitHub Pages
robots.txt, sitemap.xml, google*.html   SEO / Search Console
```

**Achtung:** GitHub Pages veröffentlicht alles im Branch, auch nicht verlinkte Dateien. Interne Dokumente nur in `docs/` ablegen (per `_config.yml` ausgeschlossen); private Belege, Logo-Pakete oder PDFs gehören gar nicht ins Repo.

## Konventionen

- **Dateinamen:** Seiten kleingeschrieben, deutsch, flach im Root (`leistungen.html`), Umlaute umschrieben (`ueber-mich.html`).
- **Kein Templating:** Header/Nav/Footer sind auf jeder Seite dupliziert. Bei Änderungen daran **alle 15 Seiten** konsistent anpassen.
- **CSS:** BEM-artige Klassennamen (`hero__title`, `nav__link--active`, `btn btn--primary`). Farben/Abstände nur über CSS-Variablen aus `:root` in [css/style.css](css/style.css). Variablennamen sind lowercase (`--color-primary`, nicht `--Color-primary`).
- **JS:** Vanilla JS, alles in [js/main.js](js/main.js), keine Libraries.
- **Neue Seite anlegen:** individuellen `<title>`, `meta description`, `rel="canonical"` und OG-Tags setzen; Nav + Footer auf **allen** Seiten ergänzen; in [sitemap.xml](sitemap.xml) eintragen.
- **Bilder:** immer mit sinnvollem `alt`-Text (Bestand ist vollständig — so halten).
- **Strukturierte Daten:** Schema.org `ProfessionalService` auf index.html, `FAQPage` auf leistungen.html und energieausweis.html — bei Adress-/Leistungs-/FAQ-Änderungen mitpflegen.
- **Datenschutz-Prinzip:** Fonts lokal, Analytics nur GoatCounter, Formular via Web3Forms. Keine Google-Fonts-, CDN- oder Tracking-Einbindungen, die Daten an Dritte senden.

## Ton & Sprache

- Deutsch, Sie-Form, seriös und kompetent, kein Marketing-Sprech.
- Fachbegriffe korrekt und konsistent: iSFP, Heizlastberechnung nach DIN EN 12831 (raumweise), hydraulischer Abgleich nach Verfahren B, Lüftungskonzept nach DIN 1946-6, Bestätigung zum Antrag (BzA), Bestätigung nach Durchführung (BnD), Technische Projektbeschreibung (TPB), Technischer Projektnachweis (TPN), BEG, Energieeffizienz-Experte (EEE).
- Antwortzeit einheitlich: „in der Regel innerhalb eines Werktags" (nicht „24 Stunden").
- Preishinweis einheitlich: „Alle Preise als Kleinunternehmer nach § 19 UStG – es fällt keine Umsatzsteuer an."

## Bekannte Besonderheiten / Stolperfallen

- **Deployment ist rein manuell** (git push). Es gibt keine Tests, keinen Linter, keine Link-Prüfung — nichts läuft automatisch.
- **FAQ doppelt gepflegt:** Die FAQs in [leistungen.html](leistungen.html) und [energieausweis.html](energieausweis.html) existieren zweimal — als JSON-LD (`FAQPage`) im `<head>` und als sichtbare Sektion. Beide müssen synchron bleiben (Google verlangt sichtbaren Inhalt für FAQ-Markup).
- **Performance:** Bilder sind komprimiert (`hero.jpg` ~123 KB, `profil.jpg` ~25 KB, `logo-weiss.png` ~13 KB) mit `width`/`height`, `loading="lazy"` und `fetchpriority="high"` am Hero-Bild. Optionaler nächster Schritt: WebP-Auslieferung.
- **Barrierefreiheit:** Skip-Link, `aria-expanded` am Mobile-Menü-Button und `aria-hidden="true"` an dekorativen Icons sind umgesetzt; bei neuen Elementen beibehalten.
- Viele Inline-Styles in den HTML-Dateien; bei größeren Umbauten schrittweise in [css/style.css](css/style.css) überführen.
- Das Repo liegt in einem OneDrive-Ordner — bei Sync-Konflikten können Duplikat-Dateien entstehen.

## Was ich NICHT möchte

- **Kein `git push` / Deploy ohne explizite Freigabe.** Commits lokal sind ok, wenn beauftragt.
- **Preise & Konditionen** (Preisboxen und Preistabelle in [leistungen.html](leistungen.html)) nur nach expliziter Freigabe ändern.
- Keine Frameworks, Bundler oder externen Abhängigkeiten einführen.
- Konkrete Förderdetails (Bonushöhen, Fristen, Programmänderungen wie z. B. eine KfW-458-Reform) gehören **nicht** in AGENTS.md oder docs/business-context.md — das ist Content und wird direkt in den Seiteninhalten gepflegt.
