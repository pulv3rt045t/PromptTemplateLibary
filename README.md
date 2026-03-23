# Claude Projekt – Template-Bibliothek

Eine Sammlung von Prompt-Templates zur automatischen Generierung von druckfertigen PDFs, strukturierten Dokumenten und Cheat-Sheets direkt aus Claude heraus.

---

## Schnellstart

Trigger-Format in einem Claude-Projekt mit dieser Bibliothek:

```
[THEMA] - [KÜRZEL]
```

**Beispiele:**
```
Python Grundlagen - Druck-Beginner-Ausfuehrlich
Git Workflow - Druck-Experte-Kompakt
SQL Basics - Web-Beginner-Ausfuehrlich
Docker Commands - Web-Experte-Kompakt
```

Claude lädt das passende Template, befüllt es mit thematisch korrektem Inhalt und liefert eine fertige PDF-Datei zum Download.

---

## Template-Kategorien

### 📄 Cheat Sheet (`docs/cheatsheet/`)

Druckfertige A4-PDF-Referenzkarten. Jedes Template enthält eine vollständige Python-Engine (reportlab) — Claude ersetzt nur den Inhalt, nie die Engine.

**8 Varianten nach 3 Dimensionen:**

| Dimension | Optionen |
|---|---|
| **Modus** | `Druck` (weißer Hintergrund) · `Web` (dunkler Hintergrund #0f0f0f) |
| **Zielgruppe** | `Beginner` (einfache Sprache) · `Experte` (Fachbegriffe, hohe Dichte) |
| **Umfang** | `Ausfuehrlich` (10–12 Einträge + Code-Box) · `Kompakt` (6–8 Einträge + Formel-Box) |

**Layout jedes Cheat-Sheets:**
- Header mit Titel und Untertitel
- 3 Karten oben (je eine Spalte)
- 2 Karten + Modifier-Pills in der Mitte
- Code-Box oder Formel-Box + Tipps-Karte unten
- Footer mit Tipp des Tages

**Alle Templates:**

| Datei | Modus | Zielgruppe | Umfang |
|---|---|---|---|
| [CS-Druck-Beginner-Ausfuehrlich.md](docs/cheatsheet/CS-Druck-Beginner-Ausfuehrlich.md) | Druck | Beginner | Ausführlich |
| [CS-Druck-Beginner-Kompakt.md](docs/cheatsheet/CS-Druck-Beginner-Kompakt.md) | Druck | Beginner | Kompakt |
| [CS-Druck-Experte-Ausfuehrlich.md](docs/cheatsheet/CS-Druck-Experte-Ausfuehrlich.md) | Druck | Experte | Ausführlich |
| [CS-Druck-Experte-Kompakt.md](docs/cheatsheet/CS-Druck-Experte-Kompakt.md) | Druck | Experte | Kompakt |
| [CS-Web-Beginner-Ausfuehrlich.md](docs/cheatsheet/CS-Web-Beginner-Ausfuehrlich.md) | Web | Beginner | Ausführlich |
| [CS-Web-Beginner-Kompakt.md](docs/cheatsheet/CS-Web-Beginner-Kompakt.md) | Web | Beginner | Kompakt |
| [CS-Web-Experte-Ausfuehrlich.md](docs/cheatsheet/CS-Web-Experte-Ausfuehrlich.md) | Web | Experte | Ausführlich |
| [CS-Web-Experte-Kompakt.md](docs/cheatsheet/CS-Web-Experte-Kompakt.md) | Web | Experte | Kompakt |

---

### 🔬 Research (`docs/research/`) — *in Entwicklung*

Templates für strukturierte Recherche-Dokumente.

---

### 📋 Summary (`docs/summary/`) — *in Entwicklung*

Templates für Zusammenfassungen und Executive Summaries.

---

### ⚙️ System (`docs/system/`) — *in Entwicklung*

System-Prompts und Konfigurations-Templates.

---

## Technische Details

**Cheat-Sheet-Engine:**
- Python + reportlab
- A4 Portrait (595×842pt)
- `draw_rows()` mit `row_mid_y`-Zentrierung
- `wrap_text()` für automatische Zeilenumbrüche
- `draw_code_box()` mit Terminal-Optik und Syntax-Highlighting
- Vollfarben: green `#1a6b00` · blue `#004fa3` · purple `#7a00b8` · red `#b80000` · orange `#b86000`

**Wichtig:** Die Engine-Funktionen dürfen nie verändert werden. Claude ersetzt ausschließlich den Block zwischen `── INHALT START ──` und `── INHALT END ──`.

---

## Projekt-Struktur

```
PromptTemplateLibary/
├── docs/
│   ├── cheatsheet/          ← 8 aktive Templates
│   ├── research/            ← in Entwicklung
│   ├── summary/             ← in Entwicklung
│   └── system/              ← in Entwicklung
├── README.md
└── PROJEKT-INSTRUKTION.md   ← Instruktion für Claude-Projekte
```

---

## Lizenz

Privates Repository – alle Rechte vorbehalten.
