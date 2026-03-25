# Claude Projekt – Template-Bibliothek

Eine Sammlung von Prompt-Templates zur automatischen Generierung von druckfertigen PDFs, HTML-Dokumenten und Cheat-Sheets direkt aus Claude heraus.

---

## Schnellstart

Im Claude-Projekt-Chat einfach aufrufen:

```
CheatSheet zu [Thema]
Vergleiche [A] vs [B]
Onepager zu [Thema]
PDF zu [Thema]
```

Claude stellt automatisch zwei kurze Abfragen — zuerst zur Themen-Präzisierung (Titel, Fokus, Ausschlüsse), dann zu den Format-Optionen (Sprache, Modus, Zielgruppe etc.) — und generiert danach die Datei.

---

## Ablauf

```
1. Aufruf     →  "CheatSheet zu Docker"
2. Abfrage 1  →  Titel / Fokus / Ausschlüsse
3. Abfrage 2  →  Sprache / Modus / Zielgruppe / Erklär-Box / ...
4. Erstellung →  Claude lädt Template, befüllt Inhalt, führt Script aus
5. Download   →  Fertige PDF oder HTML-Datei
```

---

## Verfügbare Templates

Alle produktiven Templates liegen in `docs/DocTemplates/`.

---

### 📄 Cheat Sheet
**Datei:** [`docs/DocTemplates/Template-Prompt-Cheat-Sheet-v7.md`](docs/DocTemplates/Template-Prompt-Cheat-Sheet-v7.md)

Druckfertige A4-PDF-Referenzkarten. Eine Vorlage deckt alle Varianten ab.

| Option | Auswahl |
|---|---|
| Sprache | Deutsch · Englisch · Andere |
| Ausgabe-Modus | Druck (weiß) · Web/Bildschirm (dunkel) |
| Dateiformat | PDF · HTML · Beides |
| Zielgruppe | Einsteiger · Experte |
| Umfang | Kompakt (6–8) · Ausführlich (10–12 Einträge) |
| Box unten links | Formel-Box · Kompakt-Infobox · Code-Box (nur Web) |
| Erklär-Box | Ja (empfohlen bei Einsteiger) · Nein |

```
┌─────────────────────────────────────────────────┐
│  TITEL                          Untertitel       │
├─────────────┬─────────────┬─────────────────────┤
│  Karte 1    │  Karte 2    │  Karte 3             │
│             │             │  oder Erklär-Box     │
├─────────────┼─────────────┼─────────────────────┤
│  Karte 4    │  Karte 5    │  Modifier-Pills      │
├─────────────┴─────────────┼─────────────────────┤
│  Formel- / Kompakt-Box    │  Quick Tips          │
└─────────────────────────────────────────────────┘
```

---

### ⚖️ Vergleichstabelle
**Datei:** [`docs/DocTemplates/Template-Prompt-Comparison-v1.md`](docs/DocTemplates/Template-Prompt-Comparison-v1.md)

Strukturierte Gegenüberstellung von 2–4 Optionen anhand definierter Kriterien.

| Option | Auswahl |
|---|---|
| Anzahl Optionen | 2 · 3 · 4 |
| Umfang | Kompakt (8–10 Kriterien) · Ausführlich (14–18 Kriterien) |
| Empfehlung | Ja (mit Begründung + Alternativ-Fall) · Nein |
| Erklär-Box | Ja · Nein |

---

### 📋 One-Pager
**Datei:** [`docs/DocTemplates/Template-Prompt-Onepager-v1.md`](docs/DocTemplates/Template-Prompt-Onepager-v1.md)

Einseitiges Briefing-Dokument für Pitches, Entscheidungsvorlagen und Status-Updates.

| Option | Auswahl |
|---|---|
| Zweck | Entscheidungsvorlage · Pitch · Status · Einführung |
| Struktur | Standard · Pitch (Problem→Lösung→Nutzen) · Status |
| Stil | Sachlich · Modern |
| Erklär-Box | Ja · Nein |

---

### 🗂️ PDF / HTML Basis
**Datei:** [`docs/DocTemplates/Template-Prompt-PDF-Base-v5.md`](docs/DocTemplates/Template-Prompt-PDF-Base-v5.md)

Universalvorlage für mehrseitige strukturierte Dokumente mit Abschnitten, Listen und Tabellen.

| Option | Auswahl |
|---|---|
| Layout | Karten 2-spaltig (Standard) · 1-spaltig |
| Umfang | Kompakt · Standard · Ausführlich |
| Zielgruppe | Einsteiger · Fachpublikum · Gemischt |
| Erklär-Box | Ja · Nein |

---

### 🔬 Research / 📋 Summary
**Ordner:** [`docs/DraftTemplates/`](docs/DraftTemplates/) — *Entwürfe, noch nicht produktiv*

---

## Neues Template hinzufügen

1. Datei in `docs/DocTemplates/` ablegen
2. In `docs/system/PROJEKT-INSTRUKTION.md` unter Abschnitt ① eine Zeile ergänzen:

```
TEMPLATE-NAME → https://raw.githubusercontent.com/pulv3rt045t/PromptTemplateLibary/refs/heads/main/docs/DocTemplates/Dateiname.md
```

---

## Technische Details

**Engine** (Python + reportlab, A4 Portrait 595×842pt):

| Funktion | Aufgabe |
|---|---|
| `draw_rows()` | Zeilen mit `row_mid_y`-Zentrierung und automatischem Umbruch |
| `wrap_text()` | Textwrapping innerhalb definierter Spaltenbreiten |
| `draw_erklaer_box()` | Einführungskarte für Einsteiger |
| `draw_kompakt_box()` | Helle Info-Box für Code/CLI-Themen im Druck |
| `draw_tips_card()` | Quick-Tips, garantiert formatiert (6.5pt, ratio 0.38) |
| `draw_formula_card()` | Formel-Box mit farbigen Teilen |
| `draw_comparison_table()` | Mehrspaltige Vergleichstabelle |
| `draw_naechste_schritte()` | Nummerierte Schritte-Box (One-Pager) |

Vollfarben: `green #1a6b00` · `blue #004fa3` · `purple #7a00b8` · `red #b80000` · `orange #b86000`

**Wichtigste Regel:** Engine-Funktionen nie verändern. Claude ersetzt ausschließlich den Block zwischen `── INHALT START ──` und `── INHALT END ──`.

---

## Projekt-Struktur

```
PromptTemplateLibary/
├── docs/
│   ├── DocTemplates/          ← alle produktiven Templates
│   │   ├── Template-Prompt-Cheat-Sheet-v7.md
│   │   ├── Template-Prompt-PDF-Base-v5.md
│   │   ├── Template-Prompt-Comparison-v1.md
│   │   └── Template-Prompt-Onepager-v1.md
│   ├── DraftTemplates/        ← Entwürfe, noch nicht produktiv
│   │   ├── Template-Prompt-Research-v0.md
│   │   └── Template-Prompt-Summary-v0.md
│   ├── system/
│   │   └── PROJEKT-INSTRUKTION.md
│   └── output/
│       ├── HTML/
│       └── PDF/
└── README.md
```

---

## Lizenz

Privates Repository – alle Rechte vorbehalten.
