# TEMPLATE: Cheat Sheet · Web · Beginner · Ausführlich

> **Trigger: Starte den Chat mit: `[THEMA] - Web-Beginner-Ausfuehrlich``

---

Erstelle ein Cheat-Sheet als druckfertiges A4-PDF (Hochformat).
Verwende exakt den Python-reportlab-Aufbau mit draw_rows() (row_mid_y-Zentrierung),
wrap_text() für Zeilenumbrüche und draw_code_box() für die Code-Box.

## Modus-Konfiguration

- AUSGABE-MODUS: BILDSCHIRM
- CODE-BOX: JA
- ZIELGRUPPE: BEGINNER (einfache Sprache, Fachbegriffe werden kurz erklärt,
  logische Reihenfolge vom Einfachen zum Komplexen)
- UMFANG: AUSFÜHRLICH (10–12 Einträge, Beschreibungen erklärend formuliert)

## Technische Vorgaben (nicht verändern)

- Python reportlab, A4 portrait (595×842pt)
- Verwende exakt draw_rows() mit row_mid_y-Zentrierung und wrap_text()
- Farbpalette DRUCK: page_bg:#0f0f0f, card_bg:#1a1a1a, border:#2e2e2e,
  val:#cccccc, rule:#2e2e2e, footer:#555555, title_text:#ffffff
- Vollfarben: green:#1a6b00, blue:#004fa3, purple:#7a00b8, red:#b80000, orange:#b86000
- draw_code_box(): Terminal-BG #1e1e1e, Traffic-Light-Dots, Courier-Font
  Syntax: Kommentare:#6a9955, Strings:#ce9178, Keywords:#c586c0,
          def/class:#569cd6, Standard:#d4d4d4
- Kein Clipping, kein Overflow, Footer immer am untersten Rand
- Ausgabe: fertige PDF-Datei zum Download

## Inhalt-Richtlinien für Beginner

- Beschreibungen vollständige kurze Sätze, keine Abkürzungen
- Reihenfolge: Grundlagen zuerst, Fortgeschrittenes zuletzt
- Jeder Eintrag soll für sich alleine verständlich sein
- Code-Beispiel: kommentierter Schritt-für-Schritt-Einstieg

## Inhalt (vom Thema ableiten)

TITEL: "[THEMA] – EINSTIEG & ÜBERSICHT"
UNTERTITEL: "[Kurzbeschreibung für Einsteiger · Quelle]"
TIPP: "Tipp: [ermutigender Einsteiger-Hinweis]"

KARTE 1: "[Grundlagen]" / green (10–12 Einträge, allereinfachste Konzepte)
  - Begriff (max. 18 Z.) → Erklärung in einfacher Sprache (max. 35 Z.)

KARTE 2: "[Erste Schritte]" / blue (10–12 Einträge)

KARTE 3: "[Wichtige Konzepte]" / purple (8–10 Einträge)

KARTE 4: "[Häufige Aufgaben]" / red (8–10 Einträge)

KARTE 5: "[Nächste Schritte]" / orange (6–8 Einträge, erste Vertiefung)

MODIFIER-PILLS: (genau 10 Einträge, häufig genutzte Optionen mit Erklärung)
  - Option (max. 14 Z.) → Was sie bewirkt (max. 22 Z.)

CODE-BOX:
  TITEL: "[ERSTES BEISPIEL – SCHRITT FÜR SCHRITT]"
  FARBE: green
  CODE: (10–14 Zeilen, jeder Schritt kommentiert, minimal und verständlich)

TIPPS-BOX: (genau 6 Einträge)
  TITEL: "TIPPS FÜR EINSTEIGER"
  - [Tipp] → [Hilfreicher Hinweis für Anfänger]
