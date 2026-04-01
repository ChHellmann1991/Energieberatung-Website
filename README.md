# Energieberatung Hellmann - Website

Statische Website für die Energieberatung von Christoph Hellmann.

## 🚀 Lokales Testen

```bash
# Mit Python (einfachste Methode)
python -m http.server 8000

# Dann öffnen: http://localhost:8000
```

## 📦 Deployment auf GitHub Pages

1. Dieses Repository auf GitHub pushen
2. Settings → Pages → Source: "Deploy from branch" → Branch: "main" → Ordner: "/ (root)"
3. Custom Domain: `energie-hellmann.de` eintragen
4. "Enforce HTTPS" aktivieren

## 🔧 IONOS DNS-Konfiguration

Im IONOS Kundenkonto unter Domains → energie-hellmann.de → DNS folgende Einträge hinzufügen:

| Typ | Host | Wert |
|-----|------|------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | [username].github.io |

**Wichtig:** Bestehende A-Records für @ (Root-Domain) vorher löschen!

## 📝 Web3Forms einrichten

1. Gehe zu https://web3forms.com
2. E-Mail eingeben: `kontakt@energie-hellmann.de`
3. Access Key per E-Mail erhalten
4. In `kontakt.html` den Platzhalter `YOUR_ACCESS_KEY` ersetzen

## 📁 Projektstruktur

```
website/
├── index.html          # Startseite
├── leistungen.html     # Leistungen & Preise
├── ueber-mich.html     # Über mich
├── kontakt.html        # Kontaktformular
├── impressum.html      # Impressum
├── datenschutz.html    # Datenschutzerklärung
├── CNAME               # Custom Domain für GitHub Pages
├── css/style.css       # Stylesheet
├── js/main.js          # JavaScript
└── images/             # Bilder
    ├── logo.png
    ├── profil.png
    └── hero.png
```

## ✅ Checkliste vor Go-Live

- [x] Web3Forms Access Key eingetragen
- [x] GitHub Repository erstellt
- [x] GitHub Pages aktiviert
- [ ] IONOS DNS-Einträge gesetzt (Propagation: 24-48h)
- [ ] HTTPS aktiviert
- [ ] Alle Links getestet
- [ ] Kontaktformular getestet 
