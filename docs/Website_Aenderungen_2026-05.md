# Änderungsspezifikation: energie-hellmann.de

**Erstellt:** 20. Mai 2026
**Ziel:** Die Website mit der aktuellen Akquise-Strategie (Handwerker-Partnerkanal, Gebäudehülle-Förderlogik) in Einklang bringen und zwei Selbstwidersprüche zur Geschäftsstrategie beheben.
**Umfang:** 4 bestehende HTML-Seiten (index, leistungen, ueber-mich, kontakt). Keine neuen Seiten zwingend nötig.

**Hinweis für den Agenten:** Es handelt sich um eine statische HTML-Site. Bestehendes Layout, CSS-Klassen, Icon-/Kachel-Struktur und Designsprache beibehalten. Änderungen sind rein inhaltlich plus einzelne neue Kacheln/Blöcke im vorhandenen Stil. Keine neuen Frameworks, keine Funktionsänderungen am Formular außer den unten genannten Feld-Anpassungen.

---

## Kontext: Warum diese Änderungen

Es wurden Akquise-Mails an zwei Zielgruppen verschickt:
1. **Heizungsbauer** — beworbene Leistung: Heizlastberechnung (DIN EN 12831), hydraulischer Abgleich (Verfahren B), Förderabwicklung KfW 458 (BzA/BnD).
2. **Hülle-Gewerke** (Fensterbau, Dachdecker, Stuckateur/Fassade) — beworbenes Argument: iSFP bringt dem Endkunden (a) 5 Prozentpunkte mehr BEG-Förderung und (b) Verdopplung des Förderdeckels von 30.000 € auf 60.000 € pro Wohneinheit und Kalenderjahr.

Mehrere Empfänger haben die Website besucht. Die Seite muss die Versprechen der Mails einlösen, sonst entsteht ein Bruch (Mail verspricht A, Seite zeigt B).

---

## PRIORITÄT 1 — Kritisch (Widersprüche & Kernlücke)

### 1.1 Förderdeckel 30k → 60k ergänzen (Kernlücke)

**Wo:** `leistungen.html`, Abschnitt „Individueller Sanierungsfahrplan (iSFP)" → Liste „Ihre Vorteile".

**Problem:** Das zentrale Argument der Hülle-Mails (Verdopplung des Förderdeckels) kommt auf der gesamten Website nicht vor.

**Änderung:** In der Vorteils-Liste einen neuen Listenpunkt ergänzen, im selben Format wie die bestehenden (`✓ **Titel** Beschreibung`):

```
✓ **Doppelter Förderdeckel** Mit iSFP steigt die maximal förderfähige
Summe von 30.000 € auf 60.000 € pro Wohneinheit und Jahr – entscheidend
bei größeren Maßnahmen wie Dach oder Fenstern, die meist über 30.000 € liegen.
```

Platzierung: idealerweise als zweiter Punkt, direkt nach dem „5% iSFP-Bonus", da beide thematisch zusammengehören.

---

### 1.2 Kontaktseite: „Rückruf garantiert ab 17:00 Uhr" entschärfen

**Wo:** `kontakt.html`, gelber Hinweis-Kasten am Ende der Direktkontakt-Spalte.

**Aktueller Text:**
> 💡 Hinweis: Als Ingenieur bin ich tagsüber oft in Projekten unterwegs. Bitte hinterlassen Sie eine Nachricht – ich rufe Sie garantiert ab 17:00 Uhr zurück.

**Problem:** Widerspricht der bewussten Terminsteuerung (keine standardmäßigen Abend-/Wochenend-Verpflichtungen). Die Formulierung erzieht Privatkunden auf Abendkontakt — genau das soll vermieden werden.

**Neuer Text:**
> 💡 Hinweis: Als Ingenieur bin ich tagsüber oft in Projekten unterwegs. Hinterlassen Sie mir gern eine Nachricht mit Ihrem Anliegen – ich melde mich zeitnah bei Ihnen, in der Regel innerhalb von 24 Stunden.

---

### 1.3 Kontaktformular: Erreichbarkeits-Optionen anpassen

**Wo:** `kontakt.html`, Dropdown „Wann sind Sie am besten erreichbar?".

**Aktuelle Optionen:** Morgens (9-12 Uhr) / Abends (ab 17 Uhr) / Wochenende / Jederzeit

**Problem:** „Abends" und „Wochenende" als prominente Optionen ziehen genau die Terminlagen an, die vermieden werden sollen.

**Empfohlene Änderung** (eine der beiden Varianten — Entscheidung liegt beim Betreiber):

- **Variante A (sanft):** Optionen umbenennen in: Vormittags (9–12 Uhr) / Nachmittags (13–16 Uhr) / Flexibel. „Abends" und „Wochenende" entfernen.
- **Variante B (offen lassen):** Feld ganz entfernen und stattdessen im Nachrichtenfeld-Platzhalter „Gerne Wunschtermin angeben" ergänzen. Steuerung der Termine erfolgt dann ohnehin über die Antwort-Mail / Cal.com.

> Hinweis an Betreiber: Wenn Cal.com mit auf freie Tage beschränkten Slots ohnehin der Steuerungsmechanismus ist, ist Variante B konsistenter.

---

## PRIORITÄT 2 — Wichtig (Startseite an Strategie anpassen)

### 2.1 Startseite: Verengung „nur EFH/ZFH" lockern + Handwerker-Kanal sichtbar machen

**Wo:** `index.html`, Abschnitt „Warum Ingenieurbüro Hellmann?" → Kachel „Fokus auf Wohngebäude".

**Problem:** Die Startseite ist die erste Seite, die ein klickender Handwerker sieht. Sie nennt ausschließlich „iSFP für EFH/ZFH" und erwähnt weder die Hülle-Förderlogik noch die Backoffice-Leistungen für Heizungsbauer. Der Besucher findet sein Thema nicht und springt evtl. ab, bevor er die (gute) Leistungen-Seite erreicht.

**Änderung A — bestehende Kachel umformulieren:**
Die Kachel „Fokus auf Wohngebäude" inhaltlich öffnen, ohne den WG-Schwerpunkt aufzugeben:

```
### Wohngebäude & Handwerks-Partner
Individuelle Sanierungsfahrpläne für Ein- und Zweifamilienhäuser –
sowie technische Zuarbeit (Heizlast, hydraulischer Abgleich, Förderung)
für Handwerksbetriebe der Region.
```

**Änderung B — neue Kachel oder Banner ergänzen:**
Im selben Kachel-Raster eine zusätzliche Kachel im bestehenden Stil einfügen, die direkt auf den Handwerker-Block der Leistungsseite verlinkt:

```
🤝
### Partner des Handwerks
Heizungsbauer, Dachdecker & Fensterbauer: Ich liefere iSFP, Heizlast
und hydraulischen Abgleich – fördersicher und termintreu.
→ Link zu leistungen.html#partner-handwerk
```

> Falls das Raster eine feste Kachelzahl hat (aktuell 4): entweder auf 5–6 erweitern, wenn das Layout es zulässt, oder die schwächste bestehende Kachel ersetzen. Inhaltlich am ehesten verzichtbar ist keine — besser das Raster erweitern.

---

### 2.2 Anker für Direktverlinkung setzen

**Wo:** `leistungen.html`, Abschnitt „Partner des Handwerks".

**Änderung:** Diesem Abschnitt eine ID geben (z. B. `id="partner-handwerk"`), damit von der Startseite und aus Mails direkt dorthin verlinkt werden kann.

---

### 2.3 Förderdeckel auch im Handwerker-Block nennen

**Wo:** `leistungen.html`, Abschnitt „Partner des Handwerks".

**Problem:** Der Block nennt für Hülle-Gewerke nur den „5% Förder-Bonus", nicht den verdoppelten Deckel — also nur das halbe Verkaufsargument der Mails.

**Änderung:** Den einleitenden Satz des Blocks ergänzen. Aktuell:
> Sie sanieren Dächer oder tauschen Fenster? Ich liefere den passenden iSFP inkl. 5% Förder-Bonus für Ihre Kunden.

Neu:
> Sie sanieren Dächer oder tauschen Fenster? Ich liefere den passenden iSFP für Ihre Kunden – mit 5 % Förder-Bonus und verdoppeltem Förderdeckel (60.000 € statt 30.000 € pro Jahr). So bleibt auch eine große Maßnahme voll förderfähig.

---

## PRIORITÄT 3 — Optional (Konsistenz & Feinschliff)

### 3.1 Heizungsbauer-Leistungen konkreter benennen

**Wo:** `leistungen.html`, „Partner des Handwerks", Kachel „Technische Daten inklusive".

**Optional:** „Förderabwicklung KfW 458 (BzA/BnD)" explizit ergänzen, da dies in den Heizungsbauer-Mails konkret beworben wurde. Heizungsbauer suchen genau diese Stichworte.

### 3.2 Über-mich: „Spezialisiert auf Wohngebäude (EFH/ZFH)" prüfen

**Wo:** `ueber-mich.html`, Qualifikations-Liste.

**Optional:** Der Punkt ist nicht falsch, verengt aber erneut. Erwägen, zu „Schwerpunkt Wohngebäude (EFH/ZFH)" abzuschwächen, damit kein Widerspruch zur geöffneten Startseite entsteht. Niedrige Priorität.

### 3.3 Meta-Description Startseite

**Wo:** `index.html`, `meta-description`.

**Optional:** Aktuell rein iSFP-fokussiert. Falls der Handwerker-Kanal strategisch wichtiger wird, ein Stichwort wie „Partner für Handwerksbetriebe" ergänzen. Nur relevant, wenn SEO/Auffindbarkeit später ein Thema wird — aktuell nicht dringend.

---

## NICHT ändern (bewusst so lassen)

- **Preisangaben** (1.900 € / 650 € / 1.250 €): korrekt und konsistent mit der Preisliste. Belassen.
- **4-Schritte-Ablauf** auf der Startseite: funktioniert gut für Privatkunden. Belassen.
- **dena-/Qualifikations-Signale, LiDAR/Wärmebild-Technikbetonung:** starke Vertrauensanker. Belassen.
- **Keine Erwähnung von NWG / Industrie / KMU:** bewusst nicht aufnehmen. Das Listungs- und Leistungsprofil deckt das aktuell nicht ab; verfrühte Erwähnung schafft Compliance- und Erwartungsprobleme.

---

## Zusammenfassung der Dateien & Änderungen

| Datei | Änderung | Priorität |
|-------|----------|-----------|
| `leistungen.html` | Förderdeckel-Vorteil im iSFP-Block ergänzen | 1 |
| `kontakt.html` | „Rückruf ab 17 Uhr" → „melde mich innerhalb 24h" | 1 |
| `kontakt.html` | Erreichbarkeits-Dropdown anpassen (Abend/WE raus) | 1 |
| `index.html` | Kachel „Fokus Wohngebäude" öffnen + Handwerker-Kachel ergänzen | 2 |
| `leistungen.html` | Anker `#partner-handwerk` setzen | 2 |
| `leistungen.html` | Förderdeckel im Handwerker-Block ergänzen | 2 |
| `leistungen.html` | KfW 458 / BzA / BnD ergänzen | 3 |
| `ueber-mich.html` | „Spezialisiert" → „Schwerpunkt" abschwächen | 3 |
| `index.html` | Meta-Description ergänzen | 3 |
