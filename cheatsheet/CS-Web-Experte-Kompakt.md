# TEMPLATE: Cheat Sheet · Web · Experte · Kompakt

> **Trigger: Starte den Chat mit: `[THEMA] - Web-Experte-Kompakt``

---

Erstelle ein Cheat-Sheet als druckfertiges A4-PDF (Hochformat).
Verwende exakt den Python-reportlab-Aufbau mit draw_rows() (row_mid_y-Zentrierung),
wrap_text() für Zeilenumbrüche.

## Modus-Konfiguration

- AUSGABE-MODUS: BILDSCHIRM
- CODE-BOX: NEIN → Formel-Box verwenden
- ZIELGRUPPE: EXPERTE (Fachbegriffe, dichte Informationen, keine Erklärungen)
- UMFANG: KOMPAKT (6–8 Einträge pro Karte, nur das Wesentliche)

## Technische Vorgaben (nicht verändern)

- Python reportlab, A4 portrait (595×842pt)
- Verwende exakt draw_rows() mit row_mid_y-Zentrierung und wrap_text()
- Farbpalette DRUCK: page_bg:#0f0f0f, card_bg:#1a1a1a, border:#2e2e2e,
  val:#cccccc, rule:#2e2e2e, footer:#555555, title_text:#ffffff
- Vollfarben: green:#1a6b00, blue:#004fa3, purple:#7a00b8, red:#b80000, orange:#b86000
- Kein Clipping, kein Overflow, Footer immer am untersten Rand
- Ausgabe: fertige PDF-Datei zum Download

## Layout

```
[ Karte 1     ][ Karte 2     ][ Karte 3     ]   ← Zeile 1
[ Karte 4     ][ Karte 5     ][ Modifier    ]   ← Zeile 2
[ Formel-Box (2/3 Breite)    ][ Tipps       ]   ← Zeile 3
```

## Inhalt (vom Thema ableiten)

TITEL: "[THEMA] CHEAT SHEET"
UNTERTITEL: "[Kurzbeschreibung · Quelle]"
TIPP: "Tipp: [prägnanter Experten-Merksatz]"

KARTE 1: "[Kernkategorie]" / green (6–8 Einträge, nur wichtigste Befehle/Konzepte)
  - Begriff (max. 18 Z.) → Bedeutung (max. 35 Z.)

KARTE 2: "[Kategorie]" / blue (6–8 Einträge)

KARTE 3: "[Kategorie]" / purple (6–8 Einträge)

KARTE 4: "[Kategorie]" / red (6–8 Einträge)

KARTE 5: "[Kategorie]" / orange (6–8 Einträge)

MODIFIER-PILLS: (genau 10 Einträge, wichtigste Flags/Optionen/Shortcuts)
  - Option (max. 14 Z.) → Funktion (max. 22 Z.)

FORMEL-BOX:
  LABEL: "[KERN-KONZEPT ODER WORKFLOW-FORMEL]"
  TEILE: [Schritt1/green] + [Schritt2/blue] + [Schritt3/purple] + [Schritt4/red]
  BEISPIEL: "[1–2 Zeilen konkreter Expertenanwendungsfall]"

TIPPS-BOX: (genau 6 Einträge)
  TITEL: "QUICK REFERENCE"
  - [Tipp] → [Kurz & prägnant]
