# Claude Projekt – Template-Bibliothek

Eine Sammlung von Prompt-Templates zur automatischen Generierung von druckfertigen PDFs, HTML-Dokumenten und Cheat-Sheets direkt aus Claude heraus.

---

## Schnellstart

Im Claude-Projekt-Chat einfach aufrufen:

```
CheatSheet zu [Thema]
PDF zu [Thema]
```

Claude stellt automatisch zwei kurze Abfragen — zuerst zur Themen-Präzisierung (Titel, Fokus, Ausschlüsse), dann zu den Format-Optionen (Sprache, Modus, Zielgruppe etc.) — und generiert danach die Datei.

---

## Ablauf

```
1. Aufruf im Chat  →  "CheatSheet zu Docker"
2. Abfrage 1       →  Titel / Fokus / Ausschlüsse
3. Abfrage 2       →  Sprache / Modus / Zielgruppe / Erklär-Box / ...
4. Erstellung      →  Claude lädt Template, befüllt Inhalt, führt Script aus
5. Download        →  Fertige PDF oder HTML-Datei
```

---

## Verfügbare Templates

### 📄 Cheat Sheet
**Datei:** [`docs/cheatsheet/Template-Prompt-Cheat-Sheet-v7.md`](docs/cheatsheet/Template-Prompt-Cheat-Sheet-v7.md)

Druckfertige A4-PDF-Referenzkarten. Eine Vorlage deckt alle Varianten ab — die Optionen werden per Abfrage festgelegt.

**Format-Optionen:**

| Option | Auswahl |
|---|---|
| Sprache | Deutsch · Englisch · Andere |
| Ausgabe-Modus | Druck (weiß) · Web/Bildschirm (dunkel) |
| Dateiformat | PDF · HTML · Beides |
| Zielgruppe | Einsteiger · Experte |
| Umfang | Kompakt (6–8 Einträge) · Ausführlich (10–12 Einträge) |
| Box unten links | Formel-Box · Kompakt-Infobox · Code-Box (nur Web) |
| Erklär-Box | Ja (empfohlen bei Einsteiger) · Nein |

**Layout:**

```
┌─────────────────────────────────────────────────┐
│  TITEL                          Untertitel       │
├─────────────┬─────────────┬─────────────────────┤
│  Karte 1    │  Karte 2    │  Karte 3             │
│             │             │  oder Erklär-Box     │
├─────────────┼─────────────┼─────────────────────┤
│  Karte 4    │  Karte 5    │  Modifier-Pills       │
├─────────────┴─────────────┼─────────────────────┤
│  Formel- / Kompakt-Box    │  Quick Tips          │
├─────────────────────────────────────────────────┤
│  Footer · Merksatz                               │
└─────────────────────────────────────────────────┘
```

---

### 📋 PDF / HTML Basis
**Datei:** [`docs/system/Template-Prompt-PDF-Base-v5.md`](docs/system/Template-Prompt-PDF-Base-v5.md)

Universalvorlage für strukturierte Dokumente mit Abschnitten, Listen und Tabellen. Ausgabe wahlweise als PDF, HTML oder beides.

**Format-Optionen:**

| Option | Auswahl |
|---|---|
| Sprache | Deutsch · Englisch · Andere |
| Ausgabe-Modus | Druck (weiß) · Web/Bildschirm (dunkel) |
| Dateiformat | PDF · HTML · Beides |
| Layout | Karten 2-spaltig (Standard) · 1-spaltig |
| Umfang | Kompakt · Standard · Ausführlich |
| Zielgruppe | Einsteiger · Fachpublikum · Gemischt |
| Erklär-Box | Ja (empfohlen bei Einsteiger) · Nein |

---

### 🔬 Research (`docs/research/`) — *in Entwicklung*
### 📋 Summary (`docs/summary/`) — *in Entwicklung*

---

## Neues Template hinzufügen

In `docs/system/PROJEKT-INSTRUKTION.md` unter Abschnitt ① eine neue Zeile ergänzen:

```
TEMPLATE-NAME → https://raw.githubusercontent.com/.../docs/ordner/Dateiname.md
```

Kein weiterer Aufwand — Claude erkennt das Template automatisch beim Aufruf per Name oder Thema.

---

## Technische Details

**Cheat-Sheet-Engine** (Python + reportlab, A4 Portrait 595×842pt):

| Funktion | Aufgabe |
|---|---|
| `draw_rows()` | Zeilen mit `row_mid_y`-Zentrierung und automatischem Umbruch |
| `wrap_text()` | Textwrapping innerhalb definierter Spaltenbreiten |
| `draw_erklaer_box()` | Helle Einführungskarte für Einsteiger (oben rechts) |
| `draw_kompakt_box()` | Helle Info-Box unten links für Code/CLI-Themen im Druck |
| `draw_tips_card()` | Quick-Tips, garantiert formatiert (6.5pt, ratio 0.38) |
| `draw_formula_card()` | Formel-Box mit farbigen Teilen und Beispielzeile |
| `draw_code_box()` | Terminal-Box mit Syntax-Highlighting (nur Web/HTML) |

Vollfarben: `green #1a6b00` · `blue #004fa3` · `purple #7a00b8` · `red #b80000` · `orange #b86000`

**Wichtigste Regel:** Engine-Funktionen nie verändern. Claude ersetzt ausschließlich den Block zwischen `── INHALT START ──` und `── INHALT END ──`.

---

## Projekt-Struktur

```
PromptTemplateLibary/
├── docs/
│   ├── cheatsheet/
│   │   └── Template-Prompt-Cheat-Sheet-v7.md   ← aktiv
│   ├── system/
│   │   ├── PROJEKT-INSTRUKTION.md               ← Claude-Projekt-Instruktion
│   │   └── Template-Prompt-PDF-Base-v5.md       ← aktiv
│   ├── research/                                ← in Entwicklung
│   └── summary/                                 ← in Entwicklung
└── README.md
```

---

## Lizenz

Privates Repository – alle Rechte vorbehalten.