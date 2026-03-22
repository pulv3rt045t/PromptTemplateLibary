# TEMPLATE: Cheat Sheet · Druck · Beginner · Kompakt

> **Trigger:** Starte den Chat mit: `[THEMA] - Druck-Beginner-Kompakt`

---

Erstelle ein Cheat-Sheet als druckfertiges A4-PDF (Hochformat).
Verwende exakt den Python-reportlab-Aufbau mit draw_rows() (row_mid_y-Zentrierung)
und wrap_text() für Zeilenumbrüche.

## Modus-Konfiguration

- AUSGABE-MODUS: DRUCK
- CODE-BOX: NEIN → Formel-Box verwenden
- ZIELGRUPPE: BEGINNER (einfache Sprache, nur absolut Notwendiges)
- UMFANG: KOMPAKT (6–8 Einträge pro Karte, klare Prioritäten, kein Overload)

## Technische Vorgaben (nicht verändern)

- Python reportlab, A4 portrait (595×842pt)
- Verwende exakt draw_rows() mit row_mid_y-Zentrierung und wrap_text()
- Farbpalette DRUCK: page_bg:#ffffff, card_bg:#ffffff, border:#dddddd,
  val:#333333, rule:#dddddd, footer:#999999, title_text:#ffffff
- Vollfarben: green:#1a6b00, blue:#004fa3, purple:#7a00b8, red:#b80000, orange:#b86000
- Kein Clipping, kein Overflow, Footer immer am untersten Rand
- Ausgabe: fertige PDF-Datei zum Download

## Inhalt-Richtlinien für Beginner-Kompakt

- Nur die 6–8 wichtigsten Dinge pro Kategorie
- Keine Fachbegriffe ohne kurze Erklärung
- Formel-Box zeigt den einfachsten Einstiegsweg
- Tipps: ermutigen und praktisch orientieren

## Inhalt (vom Thema ableiten)

TITEL: "[THEMA] – SCHNELLSTART"
UNTERTITEL: "[Thema einfach erklärt · Quelle]"
TIPP: "Tipp: [einfacher Merksatz für Einsteiger]"

KARTE 1: "[Das Wichtigste]" / green (6–8 Einträge, absolute Grundlagen)
  - Begriff (max. 18 Z.) → Einfache Erklärung (max. 35 Z.)

KARTE 2: "[Erste Schritte]" / blue (6–8 Einträge)

KARTE 3: "[Häufigste Aufgaben]" / purple (6–8 Einträge)

KARTE 4: "[Hilfreiche Optionen]" / red (6–8 Einträge)

KARTE 5: "[Was als Nächstes]" / orange (6 Einträge)

MODIFIER-PILLS: (genau 10 Einträge, die 10 nützlichsten Ergänzungen)
  - Option (max. 14 Z.) → Einfache Erklärung (max. 22 Z.)

FORMEL-BOX:
  LABEL: "[DER EINFACHSTE EINSTIEGSWEG]"
  TEILE: [Schritt1/green] + [Schritt2/blue] + [Schritt3/purple] + [Schritt4/red]
  BEISPIEL: "[Alltagsnahes Beispiel in 1–2 Zeilen]"

TIPPS-BOX: (genau 6 Einträge)
  TITEL: "STARTHILFE"
  - [Tipp] → [Praktisch & motivierend]
