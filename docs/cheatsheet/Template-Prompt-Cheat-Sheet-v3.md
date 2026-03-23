Erstelle mir ein Cheat-Sheet als druckfertiges A4-PDF (Hochformat)
im Stil von claude-cheatsheet-v6.pdf.

AUSGABE-MODUS: [DRUCK / BILDSCHIRM]

CODE-BOX: [JA / NEIN]
→ JA:   Ersetzt die Formel-Box (unten links, 2/3 Breite) durch
        ein dunkles Terminal-Fenster mit Syntax-Highlighting
→ NEIN: Standard Formel-Box wird verwendet

─────────────────────────────────────────────
TECHNISCHE VORGABEN (nicht verändern):
─────────────────────────────────────────────
- Python reportlab, A4 portrait (595×842pt)
- Verwende exakt draw_rows() mit row_mid_y-Zentrierung
  und wrap_text() für automatische Zeilenumbrüche
- draw_code_box() mit dunklem Terminal-BG (#1e1e1e),
  Traffic-Light-Dots, Courier-Font, Syntax-Highlighting:
    Kommentare → #6a9955 (grün)
    Strings     → #ce9178 (orange)
    Keywords    → #c586c0 (lila)
    def/class   → #569cd6 (blau)
    Standard    → #d4d4d4 (grau)
- Code-Box passt Fontgröße automatisch an Zeilenanzahl an
- Kein Clipping, kein Overflow über Seitenrand
- KEINE zusätzlichen Elemente außer den definierten Karten
- Footer IMMER am untersten Rand, nicht überlappend
- Ausgabe: fertige PDF-Datei zum Download
─────────────────────────────────────────────

Farbpalette je nach Modus:

DRUCK:
  page_bg: #ffffff   card_bg: #ffffff
  border:  #dddddd   title_text: #ffffff
  key:     Vollfarbe val: #333333
  rule:    #dddddd   footer: #999999

BILDSCHIRM:
  page_bg: #0f0f0f   card_bg: #1a1a1a
  border:  #2e2e2e   title_text: #ffffff
  key:     Vollfarbe val: #cccccc
  rule:    #2e2e2e   footer: #555555

Vollfarben (beide Modi):
  green:#1a6b00  blue:#004fa3  purple:#7a00b8
  red:#b80000    orange:#b86000

─────────────────────────────────────────────
INHALT:
─────────────────────────────────────────────

TITEL: [z.B. "PYTHON CHEAT SHEET"]
UNTERTITEL: [z.B. "Schnellreferenz · python.org"]
TIPP (Fußzeile): [z.B. "Tipp: Erst verstehen, dann anwenden"]

KARTE 1: "[TITEL]" / [green|blue|purple|red|orange]
  - Keyword (max. 18 Zeichen) → Beschreibung (max. 35 Zeichen)
  (10–12 Einträge)

KARTE 2: "[TITEL]" / [FARBE]
  (10–12 Einträge)

KARTE 3: "[TITEL]" / [FARBE]
  (8–10 Einträge)

KARTE 4: "[TITEL]" / [FARBE]
  (8–10 Einträge)

KARTE 5: "[TITEL]" / [FARBE]
  (6–8 Einträge)

MODIFIER-PILLS: (genau 10 Einträge)
  - Label (max. 14 Zeichen) → Beschreibung (max. 22 Zeichen)

─── NUR WENN CODE-BOX: JA ───────────────────
CODE-BOX:
  TITEL: "[z.B. CODE-BEISPIEL – CSV NACH JSON]"
  FARBE: [Farbe für Titelbalken]
  CODE: (max. 16 Zeilen, empfohlen 10–14)
    [Zeile 1]
    [Zeile 2]
    ...

─── NUR WENN CODE-BOX: NEIN ─────────────────
FORMEL-BOX:
  LABEL: "[FORMEL-TITEL]"
  TEILE: [Teil1/green] + [Teil2/blue] + [Teil3/purple] + [Teil4/red]
  BEISPIEL: "[Max. 2 Zeilen konkretes Beispiel]"
─────────────────────────────────────────────

TIPPS-BOX: (genau 6 Einträge)
  TITEL: "[TIPPS-TITEL]"
  - Label → Beschreibung
