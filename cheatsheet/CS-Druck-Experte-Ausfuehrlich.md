# TEMPLATE: Cheat Sheet · Druck · Experte · Ausführlich

> **Trigger:** Starte den Chat mit: `[THEMA] - Druck-Experte-Ausfuehrlich`
> Claude füllt dieses Template automatisch mit dem genannten Thema aus.

---

Erstelle ein Cheat-Sheet als druckfertiges A4-PDF (Hochformat).
Verwende exakt den Python-reportlab-Aufbau mit draw_rows() (row_mid_y-Zentrierung),
wrap_text() für Zeilenumbrüche und draw_code_box() für die Code-Box.

## Modus-Konfiguration

- AUSGABE-MODUS: DRUCK
- CODE-BOX: JA
- ZIELGRUPPE: EXPERTE (Fachbegriffe, keine Grundlagen-Erklärungen, präzise Terminologie)
- UMFANG: AUSFÜHRLICH (10–12 Einträge pro Karte, Code-Box mit 12–16 Zeilen)

## Technische Vorgaben (nicht verändern)

- Python reportlab, A4 portrait (595×842pt)
- Verwende exakt draw_rows() mit row_mid_y-Zentrierung und wrap_text()
- Farbpalette DRUCK: page_bg:#ffffff, card_bg:#ffffff, border:#dddddd,
  val:#333333, rule:#dddddd, footer:#999999, title_text:#ffffff
- Vollfarben: green:#1a6b00, blue:#004fa3, purple:#7a00b8, red:#b80000, orange:#b86000
- draw_code_box(): Terminal-BG #1e1e1e, Traffic-Light-Dots, Courier-Font
  Syntax: Kommentare:#6a9955, Strings:#ce9178, Keywords:#c586c0,
          def/class:#569cd6, Standard:#d4d4d4
- Fontgröße Code-Box automatisch an Zeilenanzahl anpassen
- Kein Clipping, kein Overflow, Footer immer am untersten Rand
- Ausgabe: fertige PDF-Datei zum Download

## Layout (3 Spalten × 3 Zeilen, fix)

```
[ Karte 1     ][ Karte 2     ][ Karte 3     ]   ← Zeile 1 (größer)
[ Karte 4     ][ Karte 5     ][ Modifier    ]   ← Zeile 2
[ Code-Box (2/3 Breite)      ][ Tipps       ]   ← Zeile 3
```

## Inhalt (vom Thema ableiten)

TITEL: "[THEMA IN GROSSBUCHSTABEN] CHEAT SHEET"
UNTERTITEL: "[Kurzbeschreibung · Quelle/Website]"
TIPP: "Tipp: [themenspezifischer Expertenhinweis]"

KARTE 1: "[Hauptkategorie]" / green (10–12 Einträge, Experten-Terminologie)
  - Fachbegriff (max. 18 Z.) → Präzise Definition (max. 35 Z.)

KARTE 2: "[Zweite Kernkategorie]" / blue (10–12 Einträge)

KARTE 3: "[Dritte Kategorie]" / purple (8–10 Einträge)

KARTE 4: "[Vierte Kategorie]" / red (8–10 Einträge)

KARTE 5: "[Fünfte Kategorie]" / orange (6–8 Einträge, fortgeschrittene Themen)

MODIFIER-PILLS: (genau 10 Einträge, themenspezifische Operatoren/Flags/Optionen)
  - Flag/Option (max. 14 Z.) → Funktion (max. 22 Z.)

CODE-BOX:
  TITEL: "[PRAXISBEISPIEL – TYPISCHER USE CASE]"
  FARBE: blue
  CODE: (12–16 Zeilen, reales Experten-Beispiel mit Kommentaren)

TIPPS-BOX: (genau 6 Einträge)
  TITEL: "BEST PRACTICES"
  - [Experten-Tipp] → [Konkrete Handlungsempfehlung]
