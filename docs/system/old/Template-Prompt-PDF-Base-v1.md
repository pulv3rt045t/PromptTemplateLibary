# TEMPLATE: PDF / HTML – Universalbasis
# Datei: Template-Prompt-PDF-Base-v1.md
# Aufruf im Chat: "PDF zu [THEMA]" oder "Template-Prompt-PDF-Base-v1"
#
# ═══════════════════════════════════════════════════════════
# ANWEISUNG AN CLAUDE – PFLICHTABLAUF:
#
# SCHRITT 1: MULTIPLE-CHOICE-ABFRAGE
# Stelle dem Nutzer VOR der Erstellung folgende Abfrage im Chat.
# Warte auf Antwort bevor du weitermachst.
#
#   Bevor ich loslege – ein paar kurze Optionen:
#
#   🌍 Sprache:        [ ] Deutsch  [ ] Englisch  [ ] Andere: ___
#   🖨️  Ausgabe-Modus:  [ ] Druck (weiß)  [ ] Bildschirm/Web (dunkel)
#   📄 Dateiformat:    [ ] PDF  [ ] HTML  [ ] Beides
#   📐 Layout:         [ ] 1-spaltig  [ ] 2-spaltig  [ ] 3-spaltig
#   🎨 Stil:           [ ] Sachlich/Clean  [ ] Modern/Farbig  [ ] Minimal
#   📏 Umfang:         [ ] Kompakt (1 Seite)  [ ] Standard (2–4 S.)  [ ] Ausführlich
#   👤 Zielgruppe:     [ ] Einsteiger  [ ] Fachpublikum  [ ] Gemischt
#
#   Weitere Details / Schwerpunkte (optional): ___________
#
# SCHRITT 2: FORMAT WÄHLEN UND ERSTELLEN
#   PDF  → Python reportlab, A4 portrait
#   HTML → Standalone HTML mit eingebettetem CSS
#   Beides → Erst PDF, dann HTML-Äquivalent
#
# SCHRITT 3: DATEI AUSFÜHREN / LIEFERN
#   PDF: pip install reportlab --break-system-packages -q
#        python script.py → present_files
#   HTML: Direkt als .html Datei speichern → present_files
# ═══════════════════════════════════════════════════════════
#
# FARBPALETTEN:
#
# DRUCK (hell):
#   Hintergrund: #ffffff  Text: #111111  Akzent: #004fa3
#   Sekundär: #1a6b00  Muted: #666666  Border: #dddddd
#
# WEB/BILDSCHIRM (dunkel):
#   Hintergrund: #0f0f0f  Text: #ffffff  Akzent: #004fa3
#   Sekundär: #1a6b00  Muted: #888888  Border: #2e2e2e
#
# VOLLFARBEN (beide Modi):
#   green:#1a6b00  blue:#004fa3  purple:#7a00b8
#   red:#b80000    orange:#b86000
# ═══════════════════════════════════════════════════════════

# ── PDF-ENGINE (für PDF-Ausgabe) ────────────────────────────
# Verwende diesen Block wenn Dateiformat=PDF gewählt wurde.
# Passe NUR den INHALT-Block an, Engine nicht verändern.

```python
# PDF-VARIANTE
from reportlab.lib.pagesizes import A4
from reportlab.pdfgen import canvas
from reportlab.lib import colors
from reportlab.lib.styles import getSampleStyleSheet
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer, Table, TableStyle
from reportlab.lib.units import mm

# ── FARBPALETTE (je nach Modus einsetzen) ──
# DRUCK (hell):
COLORS = {
    'bg':       '#ffffff',
    'text':     '#111111',
    'accent':   '#004fa3',
    'secondary':'#1a6b00',
    'muted':    '#666666',
    'border':   '#dddddd',
    'white':    '#ffffff',
}
# WEB (dunkel) – alternativ:
# COLORS = {
#     'bg':       '#0f0f0f',
#     'text':     '#ffffff',
#     'accent':   '#004fa3',
#     'secondary':'#1a6b00',
#     'muted':    '#888888',
#     'border':   '#2e2e2e',
#     'white':    '#ffffff',
# }

def hx(col): return colors.HexColor(col)

# ═══════════════════════════════════════════════
# ── INHALT START ── (NUR DIESEN BLOCK ERSETZEN)
# ═══════════════════════════════════════════════

TITEL      = '[DOKUMENTTITEL]'
UNTERTITEL = '[Kurzbeschreibung · Quelle/Datum]'
SPRACHE    = 'de'  # 'de' oder 'en'

# Abschnitte: Liste von (Titel, Inhalt-Absatz oder Liste)
ABSCHNITTE = [
    ('[ABSCHNITT 1 TITEL]', [
        '[Absatz oder Stichpunkt 1]',
        '[Absatz oder Stichpunkt 2]',
    ]),
    ('[ABSCHNITT 2 TITEL]', [
        '[Absatz oder Stichpunkt 1]',
    ]),
    # Weitere Abschnitte nach Bedarf
]

# Tabellen (optional): Liste von (Titel, Header-Zeile, Daten-Zeilen)
TABELLEN = [
    ('[TABELLENTITEL]',
     ['Spalte 1', 'Spalte 2', 'Spalte 3'],
     [
         ['Wert A1', 'Wert A2', 'Wert A3'],
         ['Wert B1', 'Wert B2', 'Wert B3'],
     ]),
]

FUSSNOTE = '[Fußzeile · Datum · Version]'

# ═══════════════════════════════════════════════
# ── INHALT END ──
# ═══════════════════════════════════════════════


# ── ENGINE (NICHT VERÄNDERN) ────────────────────────────────

def make_pdf(path):
    doc = SimpleDocTemplate(path, pagesize=A4,
                            leftMargin=18*mm, rightMargin=18*mm,
                            topMargin=18*mm, bottomMargin=18*mm)
    styles = getSampleStyleSheet()
    story  = []

    # Header
    from reportlab.platypus import Paragraph
    from reportlab.lib.styles import ParagraphStyle
    from reportlab.lib.enums import TA_LEFT, TA_CENTER

    title_style = ParagraphStyle('title', fontName='Helvetica-Bold',
                                  fontSize=18, textColor=hx(COLORS['text']),
                                  spaceAfter=4)
    sub_style   = ParagraphStyle('sub', fontName='Helvetica',
                                  fontSize=8, textColor=hx(COLORS['muted']),
                                  spaceAfter=12)
    sec_style   = ParagraphStyle('sec', fontName='Helvetica-Bold',
                                  fontSize=10, textColor=hx(COLORS['accent']),
                                  spaceBefore=10, spaceAfter=4)
    body_style  = ParagraphStyle('body', fontName='Helvetica',
                                  fontSize=8, textColor=hx(COLORS['text']),
                                  spaceAfter=3, leading=12)
    foot_style  = ParagraphStyle('foot', fontName='Helvetica',
                                  fontSize=7, textColor=hx(COLORS['muted']),
                                  alignment=TA_CENTER, spaceBefore=16)

    story.append(Paragraph(TITEL, title_style))
    story.append(Paragraph(UNTERTITEL, sub_style))

    # Trennlinie
    from reportlab.platypus import HRFlowable
    story.append(HRFlowable(width='100%', thickness=1.5,
                             color=hx(COLORS['text']), spaceAfter=8))

    # Abschnitte
    for sec_title, items in ABSCHNITTE:
        story.append(Paragraph(sec_title, sec_style))
        for item in items:
            story.append(Paragraph(f'• {item}', body_style))

    # Tabellen
    for tbl_title, header, rows in TABELLEN:
        story.append(Paragraph(tbl_title, sec_style))
        data = [header] + rows
        t = Table(data, hAlign='LEFT')
        t.setStyle(TableStyle([
            ('BACKGROUND', (0,0), (-1,0), hx(COLORS['accent'])),
            ('TEXTCOLOR',  (0,0), (-1,0), hx(COLORS['white'])),
            ('FONTNAME',   (0,0), (-1,0), 'Helvetica-Bold'),
            ('FONTSIZE',   (0,0), (-1,-1), 7.5),
            ('FONTNAME',   (0,1), (-1,-1), 'Helvetica'),
            ('TEXTCOLOR',  (0,1), (-1,-1), hx(COLORS['text'])),
            ('ROWBACKGROUNDS', (0,1), (-1,-1),
             [hx('#f5f5f5'), hx(COLORS['bg'])]),
            ('GRID', (0,0), (-1,-1), 0.4, hx(COLORS['border'])),
            ('TOPPADDING',    (0,0), (-1,-1), 3),
            ('BOTTOMPADDING', (0,0), (-1,-1), 3),
            ('LEFTPADDING',   (0,0), (-1,-1), 5),
        ]))
        story.append(t)

    story.append(Paragraph(FUSSNOTE, foot_style))
    doc.build(story)
    print(f"Done → {path}")

make_pdf('/home/claude/output.pdf')
```

# ── HTML-ENGINE (für HTML-Ausgabe) ─────────────────────────
# Verwende diesen Block wenn Dateiformat=HTML gewählt wurde.
# Passe NUR den INHALT-Block an, Engine nicht verändern.
# Speichere als .html Datei.

```python
# HTML-VARIANTE
# ═══════════════════════════════════════════════
# ── INHALT START ── (NUR DIESEN BLOCK ERSETZEN)
# ═══════════════════════════════════════════════

TITEL      = '[DOKUMENTTITEL]'
UNTERTITEL = '[Kurzbeschreibung · Quelle/Datum]'
MODUS      = 'druck'   # 'druck' oder 'web'

ABSCHNITTE = [
    ('[ABSCHNITT 1 TITEL]', [
        '[Stichpunkt oder Absatz 1]',
        '[Stichpunkt oder Absatz 2]',
    ]),
    ('[ABSCHNITT 2 TITEL]', [
        '[Stichpunkt oder Absatz 1]',
    ]),
]

TABELLEN = [
    ('[TABELLENTITEL]',
     ['Spalte 1', 'Spalte 2', 'Spalte 3'],
     [['Wert A1','Wert A2','Wert A3'],
      ['Wert B1','Wert B2','Wert B3']]),
]

FUSSNOTE = '[Fußzeile · Datum · Version]'

# ═══════════════════════════════════════════════
# ── INHALT END ──
# ═══════════════════════════════════════════════


# ── HTML ENGINE (NICHT VERÄNDERN) ───────────────────────────

def make_html(path):
    if MODUS == 'web':
        bg, text, card, border, accent, muted = \
            '#0f0f0f','#ffffff','#1a1a1a','#2e2e2e','#004fa3','#888888'
    else:
        bg, text, card, border, accent, muted = \
            '#ffffff','#111111','#f5f5f5','#dddddd','#004fa3','#666666'

    secs_html = ''
    for title, items in ABSCHNITTE:
        items_html = ''.join(f'<li>{i}</li>' for i in items)
        secs_html += f'''
        <div class="section">
          <h2>{title}</h2>
          <ul>{items_html}</ul>
        </div>'''

    tbls_html = ''
    for tbl_title, header, rows in TABELLEN:
        th = ''.join(f'<th>{h}</th>' for h in header)
        tr = ''.join(
            '<tr>' + ''.join(f'<td>{c}</td>' for c in row) + '</tr>'
            for row in rows)
        tbls_html += f'''
        <div class="section">
          <h2>{tbl_title}</h2>
          <table><thead><tr>{th}</tr></thead><tbody>{tr}</tbody></table>
        </div>'''

    html = f'''<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>{TITEL}</title>
<style>
  *, *::before, *::after {{ box-sizing: border-box; margin: 0; padding: 0; }}
  body {{ background:{bg}; color:{text}; font-family:Helvetica,Arial,sans-serif;
          font-size:13px; line-height:1.5; padding:32px; max-width:900px; margin:0 auto; }}
  header {{ border-bottom:2px solid {text}; padding-bottom:12px; margin-bottom:24px; }}
  h1 {{ font-size:22px; letter-spacing:.5px; }}
  h1 span {{ color:{muted}; font-weight:400; }}
  .subtitle {{ font-size:9px; color:{muted}; margin-top:4px; }}
  h2 {{ font-size:10px; font-weight:700; color:{accent};
        text-transform:uppercase; letter-spacing:.5px;
        margin-bottom:6px; padding-bottom:3px;
        border-bottom:1px solid {border}; }}
  .section {{ background:{card}; border:1px solid {border};
              border-radius:4px; padding:12px 14px; margin-bottom:12px; }}
  ul {{ padding-left:14px; }}
  li {{ margin-bottom:3px; font-size:12px; }}
  table {{ width:100%; border-collapse:collapse; font-size:11px; margin-top:6px; }}
  th {{ background:{accent}; color:#fff; padding:5px 8px;
        text-align:left; font-weight:700; }}
  td {{ padding:4px 8px; border-bottom:1px solid {border}; }}
  tr:nth-child(even) td {{ background:{'#252525' if MODUS=='web' else '#f9f9f9'}; }}
  footer {{ margin-top:24px; font-size:8px; color:{muted};
            text-align:center; border-top:1px solid {border}; padding-top:8px; }}
  @media print {{ body {{ padding:0; }} }}
</style>
</head>
<body>
<header>
  <h1>{' '.join(f'<span>{w}</span>' if i==1 else w for i,w in enumerate(TITEL.split()))}</h1>
  <div class="subtitle">{UNTERTITEL}</div>
</header>
{secs_html}
{tbls_html}
<footer>{FUSSNOTE}</footer>
</body>
</html>'''

    with open(path, 'w', encoding='utf-8') as f:
        f.write(html)
    print(f"Done → {path}")

make_html('/home/claude/output.html')
```
