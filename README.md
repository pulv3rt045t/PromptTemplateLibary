# Claude Projekt – Template-Bibliothek

Eine Sammlung von Prompt-Templates zur automatischen Generierung von druckfertigen PDFs, HTML-Dokumenten und Cheat-Sheets direkt aus Claude heraus.

---

## Schnellstart

Einfach im Claude-Projekt-Chat aufrufen:

```
CheatSheet zu [THEMA]
PDF zu [THEMA]
```

Claude stellt automatisch eine kurze Abfrage zu Sprache, Modus, Zielgruppe etc. — danach wird die Datei generiert und zum Download bereitgestellt.

---

## Verfügbare Templates

### 📄 Cheat Sheet (`docs/cheatsheet/Template-Prompt-Cheat-Sheet-v4.md`)

Druckfertige A4-PDF-Referenzkarten. Eine Vorlage deckt alle Varianten ab — die gewünschten Optionen werden vor der Erstellung per Abfrage festgelegt.

**Optionen (werden vor Erstellung abgefragt):**

| Option | Auswahl |
|---|---|
| Sprache | Deutsch · Englisch · Andere |
| Ausgabe-Modus | Druck (weiß) · Bildschirm/Web (dunkel) |
| Dateiformat | PDF · HTML · Beides |
| Zielgruppe | Einsteiger · Experte |
| Umfang | Kompakt (6–8 Einträge) · Ausführlich (10–12 Einträge) |
| Box unten links | Formel-Box (Standard) · Code-Box |

**Layout:**
- Header mit Titel und Untertitel
- 3 Karten oben (je eine Spalte)
- 2 Karten + Modifier-Pills in der Mitte
- Formel-Box oder Code-Box + Tipps-Karte unten
- Footer mit Merksatz

---

### 📋 PDF / HTML Basis (`docs/cheatsheet/Template-Prompt-PDF-Base-v2.md`)

Universalvorlage für strukturierte Dokumente mit Abschnitten und Tabellen. Ausgabe wahlweise als PDF, HTML oder beides.

**Optionen (werden vor Erstellung abgefragt):**

| Option | Auswahl |
|---|---|
| Sprache | Deutsch · Englisch · Andere |
| Ausgabe-Modus | Druck (weiß) · Bildschirm/Web (dunkel) |
| Dateiformat | PDF · HTML · Beides |
| Layout | 1-spaltig · 2-spaltig · 3-spaltig |
| Stil | Sachlich/Clean · Modern/Farbig · Minimal |
| Umfang | Kompakt (1 Seite) · Standard (2–4 S.) · Ausführlich |

---

### 🔬 Research (`docs/research/`) — *in Entwicklung*
### 📋 Summary (`docs/summary/`) — *in Entwicklung*
### ⚙️ System (`docs/system/`) — Projekt-Instruktion & Konfiguration

---

## Neues Template hinzufügen

In der `PROJEKT-INSTRUKTION.md` unter Abschnitt ① einfach eine neue Zeile ergänzen:

```
TEMPLATE-NAME → https://raw.githubusercontent.com/.../docs/ordner/Dateiname.md
```

Kein weiterer Aufwand — Claude erkennt das Template automatisch beim Aufruf per Dateiname oder Thema.

---

## Technische Details

**Engine (Cheat Sheet):**
- Python + reportlab, A4 Portrait (595×842pt)
- `draw_rows()` mit `row_mid_y`-Zentrierung und `wrap_text()` für automatischen Zeilenumbruch
- `draw_formula_card()` für die Formel-Box (Standard)
- `draw_code_box()` mit Terminal-Optik und Syntax-Highlighting (optional)
- Vollfarben: green `#1a6b00` · blue `#004fa3` · purple `#7a00b8` · red `#b80000` · orange `#b86000`

**Wichtigste Regel:** Engine-Funktionen nie verändern. Claude ersetzt ausschließlich den Block zwischen `── INHALT START ──` und `── INHALT END ──`.

---

## Projekt-Struktur

```
PromptTemplateLibary/
├── docs/
│   ├── cheatsheet/
│   │   ├── Template-Prompt-Cheat-Sheet-v4.md   ← aktive Vorlage
│   │   └── Template-Prompt-PDF-Base-v2.md       ← aktive Vorlage
│   ├── research/                                ← in Entwicklung
│   ├── summary/                                 ← in Entwicklung
│   └── system/
│       └── PROJEKT-INSTRUKTION.md               ← Claude-Projekt-Instruktion
└── README.md
```

---

## Lizenz

Privates Repository – alle Rechte vorbehalten.