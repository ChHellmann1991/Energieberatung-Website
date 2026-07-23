# SEO-Plan (Schwerpunkt lokale Sichtbarkeit)

Stand: 2026-07-23 · Basis: Analyse aller 8 HTML-Seiten, sitemap.xml, robots.txt, images/

---

## 1. Befund

### Was schon gut ist

- Saubere technische Basis: canonical, OG-Tags, `lang="de"`, sitemap.xml, robots.txt, Search Console verifiziert
- Schema.org vorhanden: `ProfessionalService` (index), `FAQPage` (leistungen, energieausweis)
- Eigene Landingpage für ein Money-Keyword (energieausweis.html) — richtiges Muster
- Echte Inhalte statt Textwüste, Preise transparent, Fachbegriffe korrekt → gute Grundlage für E-E-A-T
- NAP (Name/Adresse/Telefon) auf jeder Seite im Footer, konsistent geschrieben
- Datenschutzkonform ohne externe Ressourcen (Fonts lokal) — keine Ranking-Bremse durch Consent-Layer

### Die Lücken, nach Wirkung sortiert

**A. Regionale Reichweite endet an der Stadtgrenze Böblingen** (größter Hebel)

Ortsnennungen pro Seite:

| Ort | index | leistungen | partner | ueber-mich | kontakt | energieausweis |
|---|---|---|---|---|---|---|
| Böblingen | 11 | 4 | 7 | 8 | 5 | 5 |
| Sindelfingen | 1 | 0 | 1 | 2 | 0 | 0 |
| Herrenberg | 0 | 0 | 0 | 2 | 0 | 0 |
| Holzgerlingen | 0 | 0 | 0 | 2 | 0 | 0 |
| Leonberg | 0 | 0 | 0 | 1 | 0 | 0 |
| Stuttgart | 0 | 0 | 0 | 3 | 0 | 0 |

Für „Energieberater Sindelfingen", „Energieberater Herrenberg" usw. gibt es faktisch keine Landingpage. Google zeigt im Local Pack primär Betriebe mit Sitz oder starkem Ortsbezug — ohne Ortsseiten fällt das Einzugsgebiet weg. Orte, die noch komplett fehlen, aber im Radius liegen: Ehningen, Schönaich, Weil im Schönbuch, Magstadt, Renningen, Gäufelden, Waldenbuch, Altdorf.

**B. LocalBusiness-Markup ist zu dünn**

`ProfessionalService` in [index.html](../index.html) enthält nur name, description, url, email, address, areaServed, priceRange. Es fehlen die Felder, die Google für lokale Entitäten auswertet:
`telephone`, `geo`, `sameAs` (→ Google-Business-Profil, GIH, dena-Liste), `image`/`logo`, `openingHoursSpecification`, `founder`, `hasOfferCatalog`, `@id` als stabile Entitäts-ID.

Zusätzlich fehlt komplett: `BreadcrumbList` (alle Seiten), `Service`/`Offer` auf leistungen.html, `Person` auf ueber-mich.html, `ContactPage` auf kontakt.html.

**C. Keine Verknüpfung Website ↔ Google-Business-Profil**

Kein einziger Link zum GBP, zu Google Maps oder zu Bewertungen — auf keiner Seite. Es gibt auch keine Kundenstimmen/Referenzen auf der Website. Damit fehlt Google das Signal, dass Website und Profil dieselbe Entität sind, und Besuchern der Social Proof.

**D. HTML-Fehler im `<head>` der Startseite**

[index.html:7-9](../index.html#L7): Dem `<meta name="description">` fehlt das schließende `>`. Der Parser zieht dadurch das nachfolgende `<meta name="author">` mit in dasselbe Tag — der Author-Tag existiert im DOM nicht. Die Description selbst überlebt, aber das ist ein echter Fehler im wichtigsten Head der Website.

**E. Titles/Descriptions ohne Ortsbezug auf drei Seiten**

- `Kontakt | Energieberatung Hellmann` — ohne „Böblingen"
- `Über mich | Energieberatung Hellmann` — ohne Ort, obwohl die Seite die stärkste E-E-A-T-Seite ist
- impressum.html und datenschutz.html: keine `meta description`, kein `canonical`, keine OG-Tags

**F. Content-Lücken mit Suchvolumen**

- § 35c EStG-Bescheinigung (Steuerbonus Sanierung) — wird angeboten, steht nirgends auf der Website
- „KfW 458" / „KfW 458 Antrag" — kommt im Content nicht vor (nur „KfW-Heizungsförderung")
- Kein Ratgeber-/Wissensbereich für informationale Suchen („Wärmepumpe Heizlast zu hoch", „hydraulischer Abgleich Pflicht", „iSFP Kosten")

**G. Performance / Core Web Vitals**

- `hero.png` 940 KB, wird als LCP-Element geladen — ohne `fetchpriority="high"`, ohne WebP
- `logo_weiß.png` 198 KB bei 1024×1024 px, dargestellt in Header-Größe; dient zugleich als Favicon
- `EE_EnergieeffizienzExperten_Logo.jpg` 155 KB, dreifach pro Seite eingebunden
- `profil.png` 303 KB
- Mobile LCP ist damit fast sicher jenseits der 2,5-s-Schwelle. Für lokale Suchen (überwiegend mobil) relevant.

**H. Kleinigkeiten**

- Dateiname `images/logo_weiß.png` enthält einen Umlaut → URL-Encoding-Risiko beim Crawling; sauberer wäre `logo-weiss.png`
- sitemap.xml: impressum/datenschutz fehlen (unkritisch, aber Vollständigkeit schadet nicht)
- Kein `sameAs`-Netz, keine Verzeichniseinträge erkennbar

---

## 2. Plan

### Phase 0 — Technische Fixes (ca. 1 h, sofort)

1. `<meta name="description">` in index.html schließen
2. Titles/Descriptions mit Ortsbezug schärfen:
   - kontakt.html → `Kontakt | Energieberater Böblingen – Ingenieurbüro Hellmann`
   - ueber-mich.html → `Christoph Hellmann – Energieberater in Böblingen (dena-gelistet)`
3. impressum.html + datenschutz.html: `meta description`, `canonical`, `robots noindex,follow` ergänzen (rechtliche Seiten müssen nicht ranken, sollen aber sauber sein)
4. Bild `logo_weiß.png` → `logo-weiss.png` umbenennen, Referenzen auf allen 8 Seiten anpassen

### Phase 1 — Local-SEO-Fundament (ca. 2–3 h)

5. **`ProfessionalService`-Schema ausbauen** (index.html), zusätzlich:
   ```
   "@id": "https://www.energie-hellmann.de/#organization",
   "telephone": "+4915203826121",
   "geo": { "@type": "GeoCoordinates", "latitude": ..., "longitude": ... },
   "sameAs": [ GBP-URL, GIH-Profil, dena-Expertenliste-Eintrag ],
   "logo" / "image": absolute URL,
   "openingHoursSpecification": Mo–Fr Bürozeiten,
   "founder": { "@type": "Person", "name": "Christoph Hellmann" },
   "areaServed": erweitern auf alle Orte des Einzugsgebiets,
   "hasOfferCatalog": Heizungstausch-Paket, iSFP, Baubegleitung, Energieausweis, Einzelleistungen
   ```
6. **Schema auf die anderen Seiten bringen:** `BreadcrumbList` auf alle Unterseiten, `Person` (mit `knowsAbout`, `hasCredential`) auf ueber-mich.html, `Service`-Objekte auf leistungen.html, `ContactPage` auf kontakt.html. Alle mit `"provider": {"@id": ".../#organization"}` auf die Haupt-Entität verweisen.
7. **GBP mit der Website verknüpfen:** Link zum Google-Business-Profil in Footer und auf kontakt.html, Bewertungs-Widget/Block mit echten Rezensionen (nur echte, keine erfundenen — `aggregateRating`-Markup ist ohne verifizierbare Bewertungen ein Verstoß gegen Googles Richtlinien).
8. **Einzugsgebiet sichtbar machen:** auf kontakt.html einen Block „Mein Einzugsgebiet" mit allen Orten und internen Links auf die künftigen Ortsseiten. Optional statische Karte (kein Google-Maps-iFrame — würde das Datenschutz-Prinzip brechen).

### Phase 2 — Ortsseiten (der Hauptteil, ca. 1 Seite pro Stunde)

9. Je eine Landingpage pro Kernort, Priorität nach Einwohnerzahl × Distanz:
   1. `energieberatung-sindelfingen.html`
   2. `energieberatung-herrenberg.html`
   3. `energieberatung-leonberg.html`
   4. `energieberatung-holzgerlingen.html`
   5. später: Ehningen, Schönaich, Weil im Schönbuch, Magstadt, Renningen

   **Wichtig:** Diese Seiten dürfen keine Textklone mit ausgetauschtem Ortsnamen sein — das wertet Google als Doorway Pages ab und kann die ganze Domain treffen. Jede Seite braucht echten Ortsbezug:
   - typische Bausubstanz/Baujahre und Siedlungsstruktur des Orts
   - konkrete durchgeführte Projekte (anonymisiert: „Reihenhaus Bj. 1972 in Sindelfingen-Maichingen")
   - Anfahrt/Entfernung, örtliche Besonderheiten (Fernwärmenetz, Bebauungspläne, kommunale Förderprogramme)
   - ortsspezifische FAQ

   Wenn dieser Aufwand für einen Ort nicht leistbar ist: Seite lieber weglassen, als dünn zu bauen.

10. Jede Ortsseite: eigener Title/Description/canonical/OG, `ProfessionalService` mit `areaServed` = Ort, `BreadcrumbList`, Eintrag in sitemap.xml, Verlinkung aus dem Einzugsgebiet-Block auf kontakt.html und untereinander.

### Phase 3 — Off-Page & GBP (überwiegend deine Aufgabe, nicht Code)

11. **GBP-Optimierung** (dort liegt der Großteil des lokalen Rankings):
    - Hauptkategorie prüfen: „Energieberater" — dazu Nebenkategorien wie „Ingenieurbüro", „Bauberater"
    - Da der Firmensitz eine Privatadresse ist: Adresse ausblenden und stattdessen **Einzugsgebiet** (Service Area) mit allen Orten pflegen. Ein sichtbarer Wohnsitz kann bei Prüfungen zum Problem werden und wirkt gegenüber Premium-Kunden schwächer.
    - Leistungen einzeln anlegen (Heizlastberechnung, hydraulischer Abgleich, iSFP, Energieausweis, Förderservice, § 35c-Bescheinigung) — je mit Beschreibung
    - Produkte/Preise mit Festpreisen einpflegen
    - Fotos regelmäßig ergänzen (LiDAR-Aufmaß, Wärmebild, Berichte) — Aktivität ist ein Ranking-Faktor
    - GBP-Beiträge: alle 2–4 Wochen einer, thematisch an Förderthemen gekoppelt
    - **Bewertungen:** systematischer Prozess. Nach jedem abgeschlossenen Auftrag eine Bitte per E-Mail mit direktem Bewertungslink. Ziel: 10–15 Rezensionen im ersten Halbjahr. Das ist der stärkste einzelne Local-Pack-Faktor, den du beeinflussen kannst.
    - Fragen & Antworten im Profil selbst befüllen (die vier häufigsten Kundenfragen)

12. **Citations/Verzeichnisse** — NAP überall exakt identisch (Schreibweise „Ingenieurbüro Hellmann", „Zeisigweg 17/2", „+49 152 038 26 121"):
    - dena-Energieeffizienz-Expertenliste (Profil vollständig, Website verlinkt)
    - GIH-Bundesverband-Mitgliederverzeichnis
    - Handwerkskammer-/IHK-Verzeichnis Region Stuttgart
    - Gelbe Seiten, Das Örtliche, 11880, Cylex, Wer liefert was
    - Bing Places, Apple Business Connect (wird für Apple Maps/Siri zunehmend relevant)
    - Regionale Portale: Stadtportale Böblingen/Sindelfingen, Kreishandwerkerschaft

13. **Lokale Backlinks** (Qualität vor Menge):
    - Partner-Handwerksbetriebe: gegenseitige Verlinkung auf den Partnerseiten — passt exakt zum bestehenden Partner-Konzept und ist der naheliegendste Link-Kanal
    - Lokalpresse (Kreiszeitung Böblinger Bote, Sindelfinger Zeitung): Fachbeitrag zu Förderänderungen anbieten
    - Vorträge bei VHS Böblingen / Bürgerenergiegenossenschaft → Verlinkung im Veranstaltungskalender

### Phase 4 — Content-Ausbau (fortlaufend)

14. § 35c EStG-Bescheinigung als eigener Abschnitt auf leistungen.html + eigene Landingpage, wenn sie sich rechnet
15. „KfW 458" als Begriff in den Förderservice-Content aufnehmen (Nutzer suchen die Programmnummer)
16. Ratgeber-Bereich (`ratgeber/` mit 4–6 Artikeln zum Start), jeder auf eine echte Kundenfrage aus [docs/business-context.md](business-context.md):
    - „Ist meine Wärmepumpe richtig dimensioniert? Heizlast statt Faustformel"
    - „Fenstertausch: Wann ist ein Lüftungskonzept Pflicht?"
    - „Selbst dämmen und trotzdem Förderung bekommen"
    - „iSFP oder Einzelmaßnahme — was lohnt sich wann?"
    Jeder Artikel mit `Article`-Schema, Autoren-Verweis auf die Person-Entität, interne Links auf die passende Leistung.

### Phase 5 — Performance (ca. 2 h, spätestens vor Phase 2 fertig)

17. Alle Bilder als WebP neu ausspielen, PNG als Fallback nur wo nötig; Zielgrößen: hero < 120 KB, Logo < 20 KB, Profilbild < 60 KB
18. `fetchpriority="high"` + `decoding="async"` am Hero-Bild, `loading="lazy"` an allem unterhalb des Folds (teilweise schon vorhanden)
19. Separates kleines Favicon (32×32/180×180) statt des 1024er-Logos
20. Danach messen: PageSpeed Insights für index, leistungen, energieausweis — Mobile-Wert dokumentieren

---

## 3. Reihenfolge und Aufwand

| Phase | Aufwand | Wirkung | Wann |
|---|---|---|---|
| 0 Technische Fixes | ~1 h | gering, aber Pflicht | sofort |
| 1 Schema + GBP-Verknüpfung | 2–3 h | hoch | diese Woche |
| 5 Performance | ~2 h | mittel (mobil hoch) | diese Woche |
| 3 GBP + Bewertungen | laufend | **am höchsten** | ab sofort, dauerhaft |
| 2 Ortsseiten | 1 h/Seite | hoch | über 4–6 Wochen |
| 4 Content/Ratgeber | 2–3 h/Artikel | mittel, langfristig | fortlaufend |

Ehrlich eingeordnet: Für das **Local Pack** (die Kartenergebnisse) entscheidet überwiegend das Google-Business-Profil — Bewertungen, Kategorien, Aktivität, Entfernung des Suchenden. Da ist Phase 3 der Hebel, nicht der Code. Für die **organischen Treffer darunter** entscheidet die Website — da sind Phase 1 und 2 der Hebel. Beides zusammen ergibt die Sichtbarkeit; keins der beiden allein reicht.

## 4. Messung

- Search Console: „Leistung" nach Suchanfragen filtern auf Ortsnamen, Baseline heute festhalten
- GBP-Insights: Aufrufe, Anrufe, Routenanfragen, Website-Klicks — monatlich notieren
- Manuelle Rankingprüfung im Inkognito-Fenster für: „Energieberater Böblingen", „Energieberatung Sindelfingen", „iSFP Böblingen", „Heizlastberechnung Böblingen", „Energieausweis Böblingen" — alle 4 Wochen
- GoatCounter: Einstiegsseiten der neuen Ortsseiten beobachten
- Nach jeder Phase: Rich-Results-Test für die geänderten Seiten
