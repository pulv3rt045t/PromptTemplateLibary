# TEMPLATE: PDF / HTML – Universalbasis
# Datei: Template-Prompt-PDF-Base-v5.md
# Aufruf im Chat: "PDF zu [THEMA]"
#
# ABLAUF: Siehe PROJEKT-INSTRUKTION (Abfrage 1 + 2 dort definiert)
#
# TEMPLATE-SPEZIFISCHE ZUSATZ-OPTIONEN (in Abfrage 2 ergänzen):
#   📐 Layout:   [ ] Karten 2-spaltig (Standard)  [ ] 1-spaltig
#   📏 Umfang:   [ ] Kompakt (1 Seite)  [ ] Standard (2–4 S.)  [ ] Ausführlich
#
# OPTIONEN ANWENDEN:
#   Druck/Web  → COLORS-Dict hell/dunkel (Variante auskommentiert vorhanden)
#   Karten     → LAYOUT = 'cards'   (Standard)
#   1-spaltig  → LAYOUT = 'single'
#   Einsteiger → ERKLAER_BOX befüllen  |  Experte → None
#   PDF        → ersten Python-Block verwenden (reportlab)
#   HTML       → zweiten Python-Block verwenden
#   Beides     → beide Blöcke ausführen
#
# FARBPALETTEN:
#   DRUCK:  bg:#ffffff  text:#111111  accent:#004fa3  border:#dddddd  card:#f5f5f5
#   WEB:    bg:#0f0f0f  text:#ffffff  accent:#4d9fff  border:#2e2e2e  card:#1a1a1a
#   FARBEN: green:#1a6b00  blue:#004fa3  purple:#7a00b8
#           red:#b80000    orange:#b86000
#
# ZEICHENLIMITS:
#   Stichpunkt: max. 70 Z. (single) / max. 40 Z. (cards)
#   Abschnittstitel: max. 30 Z.  |  Tabellenzelle: max. 25 Z.
#
# ENGINE NIEMALS VERÄNDERN – nur INHALT START/END Block ersetzen.
# ═══════════════════════════════════════════════════════════

```python
# PDF-VARIANTE
from reportlab.lib.pagesizes import A4
from reportlab.pdfgen import canvas
from reportlab.lib import colors
from reportlab.lib.styles import ParagraphStyle
from reportlab.lib.enums import TA_CENTER, TA_LEFT
from reportlab.platypus import SimpleDocTemplate, Paragraph, Table, TableStyle, HRFlowable, Spacer, KeepTogether
from reportlab.lib.units import mm

# ── FARBPALETTE (je nach Modus einsetzen) ──
# DRUCK (hell):
COLORS = {
    'bg': '#ffffff', 'text': '#111111', 'accent': '#004fa3',
    'accent2': '#1a6b00', 'muted': '#666666', 'border': '#dddddd',
    'card': '#f5f5f5', 'white': '#ffffff', 'header_bg': '#004fa3',
}
# WEB (dunkel) – alternativ einkommentieren:
# COLORS = {
#     'bg': '#0f0f0f', 'text': '#ffffff', 'accent': '#4d9fff',
#     'accent2': '#4dbb4d', 'muted': '#888888', 'border': '#2e2e2e',
#     'card': '#1a1a1a', 'white': '#ffffff', 'header_bg': '#1a3a6b',
# }

def hx(col): return colors.HexColor(col)

# QUALITÄTSVORGABEN – STRIKT EINHALTEN:
#   Stichpunkte:      max. 70 Zeichen (1-spaltig) / max. 40 Zeichen (2-spaltig)
#   Abschnittstitel:  max. 30 Zeichen
#   Tabellenzellen:   max. 25 Zeichen
#   Tabellenheader:   max. 15 Zeichen
#   Parallelstruktur: alle Stichpunkte eines Abschnitts gleich aufgebaut
# ═══════════════════════════════════════════════
# ── INHALT START ── (NUR DIESEN BLOCK ERSETZEN)
# ═══════════════════════════════════════════════

TITEL      = '[DOKUMENTTITEL]'
UNTERTITEL = '[Kurzbeschreibung · Quelle/Datum]'
LAYOUT     = 'cards'    # 'single' | 'two-col' | 'cards'
SPRACHE    = 'de'       # 'de' | 'en'

# Abschnitte: (Titel, Farbe, [Stichpunkte])
# Farbe nur relevant bei LAYOUT='cards': 'blue'|'green'|'purple'|'red'|'orange'|'gray'
ABSCHNITTE = [
    ('[ABSCHNITT 1]', 'blue', [
        '[Stichpunkt 1 – max. 70 Z. (single) / 40 Z. (cards/two-col)]',
        '[Stichpunkt 2]',
        '[Stichpunkt 3]',
    ]),
    ('[ABSCHNITT 2]', 'green', [
        '[Stichpunkt 1]',
        '[Stichpunkt 2]',
    ]),
    ('[ABSCHNITT 3]', 'purple', [
        '[Stichpunkt 1]',
    ]),
    ('[ABSCHNITT 4]', 'red', [
        '[Stichpunkt 1]',
    ]),
    # Weitere Abschnitte nach Bedarf
]

# Tabellen (optional): (Titel, Farbe, [Header], [[Zeilen]])
TABELLEN = [
    ('[TABELLENTITEL]', 'blue',
     ['[Header 1]', '[Header 2]', '[Header 3]'],
     [
         ['[Wert A1]', '[Wert A2]', '[Wert A3]'],
         ['[Wert B1]', '[Wert B2]', '[Wert B3]'],
     ]),
]

FUSSNOTE = '[Fußzeile · Datum · Version]'

# ═══════════════════════════════════════════════
# ── INHALT END ──
# ═══════════════════════════════════════════════


# ── ENGINE (NICHT VERÄNDERN) ────────────────────────────────

ACCENT_COLORS = {
    'blue':   '#004fa3', 'green':  '#1a6b00', 'purple': '#7a00b8',
    'red':    '#b80000', 'orange': '#b86000', 'gray':   '#555555',
}

def make_styles():
    return {
        'title':   ParagraphStyle('title', fontName='Helvetica-Bold', fontSize=18,
                                   textColor=hx(COLORS['text']), spaceAfter=3),
        'sub':     ParagraphStyle('sub', fontName='Helvetica', fontSize=8,
                                   textColor=hx(COLORS['muted']), spaceAfter=10),
        'sec':     ParagraphStyle('sec', fontName='Helvetica-Bold', fontSize=9,
                                   textColor=hx(COLORS['white']), spaceAfter=0),
        'body':    ParagraphStyle('body', fontName='Helvetica', fontSize=8,
                                   textColor=hx(COLORS['text']), spaceAfter=2, leading=11),
        'foot':    ParagraphStyle('foot', fontName='Helvetica', fontSize=7,
                                   textColor=hx(COLORS['muted']), alignment=TA_CENTER, spaceBefore=10),
        'tbl_sec': ParagraphStyle('tbl_sec', fontName='Helvetica-Bold', fontSize=9,
                                   textColor=hx(COLORS['accent']), spaceBefore=8, spaceAfter=3),
    }

def make_table(header, rows, accent_col):
    ac = ACCENT_COLORS.get(accent_col, COLORS['accent'])
    data = [header] + rows
    t = Table(data, hAlign='LEFT', repeatRows=1)
    t.setStyle(TableStyle([
        ('BACKGROUND', (0,0), (-1,0), hx(ac)),
        ('TEXTCOLOR',  (0,0), (-1,0), hx(COLORS['white'])),
        ('FONTNAME',   (0,0), (-1,0), 'Helvetica-Bold'),
        ('FONTSIZE',   (0,0), (-1,-1), 7.5),
        ('FONTNAME',   (0,1), (-1,-1), 'Helvetica'),
        ('TEXTCOLOR',  (0,1), (-1,-1), hx(COLORS['text'])),
        ('ROWBACKGROUNDS', (0,1), (-1,-1), [hx(COLORS['card']), hx(COLORS['bg'])]),
        ('GRID',       (0,0), (-1,-1), 0.4, hx(COLORS['border'])),
        ('TOPPADDING',    (0,0), (-1,-1), 3),
        ('BOTTOMPADDING', (0,0), (-1,-1), 3),
        ('LEFTPADDING',   (0,0), (-1,-1), 5),
        ('ROWBACKGROUNDS', (0,0), (0,0), [hx(ac)]),
    ]))
    return t

def build_cards_layout(story, styles, W, margins):
    """Karten-Layout: 2 Spalten, Abschnitte als farbige Karten."""
    usable_w = W - margins['left'] - margins['right']
    gap = 8
    card_w = (usable_w - gap) / 2

    def make_card(title, accent_col, items):
        ac = ACCENT_COLORS.get(accent_col, COLORS['accent'])
        header_style = ParagraphStyle('ch', fontName='Helvetica-Bold', fontSize=8,
                                       textColor=hx(COLORS['white']), spaceAfter=0,
                                       backColor=hx(ac), borderPadding=(3,6,3,6))
        item_style = ParagraphStyle('ci', fontName='Helvetica', fontSize=7.5,
                                     textColor=hx(COLORS['text']), spaceAfter=1,
                                     leading=10, leftIndent=4)
        elems = [Paragraph(title, header_style)]
        for item in items:
            elems.append(Paragraph(f'• {item}', item_style))
        inner = Table([[e] for e in elems],
                      colWidths=[card_w - 10],
                      hAlign='LEFT')
        inner.setStyle(TableStyle([
            ('BACKGROUND', (0,0), (-1,0), hx(ac)),
            ('BACKGROUND', (0,1), (-1,-1), hx(COLORS['card'])),
            ('BOX',  (0,0), (-1,-1), 0.6, hx(COLORS['border'])),
            ('TOPPADDING',    (0,0), (-1,0), 4),
            ('BOTTOMPADDING', (0,0), (-1,0), 4),
            ('LEFTPADDING',   (0,0), (-1,-1), 6),
            ('TOPPADDING',    (0,1), (-1,-1), 2),
            ('BOTTOMPADDING', (0,1), (-1,-1), 2),
        ]))
        return inner

    # Pair sections into 2-column rows
    sections = ABSCHNITTE
    for i in range(0, len(sections), 2):
        left = make_card(*sections[i])
        if i + 1 < len(sections):
            right = make_card(*sections[i+1])
            row = Table([[left, right]], colWidths=[card_w, card_w],
                        hAlign='LEFT', spaceBefore=gap)
            row.setStyle(TableStyle([
                ('LEFTPADDING',  (0,0), (-1,-1), 0),
                ('RIGHTPADDING', (0,0), (-1,-1), 0),
                ('TOPPADDING',   (0,0), (-1,-1), 0),
                ('BOTTOMPADDING',(0,0), (-1,-1), 0),
                ('INNERGRID',    (0,0), (-1,-1), 0, colors.white),
                ('ALIGN',        (0,0), (-1,-1), 'LEFT'),
                ('VALIGN',       (0,0), (-1,-1), 'TOP'),
            ]))
        else:
            row = Table([[left, '']], colWidths=[card_w, card_w],
                        hAlign='LEFT', spaceBefore=gap)
            row.setStyle(TableStyle([
                ('LEFTPADDING',  (0,0), (-1,-1), 0),
                ('RIGHTPADDING', (0,0), (-1,-1), 0),
                ('TOPPADDING',   (0,0), (-1,-1), 0),
                ('BOTTOMPADDING',(0,0), (-1,-1), 0),
                ('ALIGN',        (0,0), (-1,-1), 'LEFT'),
                ('VALIGN',       (0,0), (-1,-1), 'TOP'),
            ]))
        story.append(row)

def build_single_layout(story, styles):
    for sec_title, accent_col, items in ABSCHNITTE:
        ac = ACCENT_COLORS.get(accent_col, COLORS['accent'])
        sec_s = ParagraphStyle('s', fontName='Helvetica-Bold', fontSize=9,
                                textColor=hx(COLORS['white']), backColor=hx(ac),
                                spaceBefore=8, spaceAfter=0,
                                borderPadding=(3,6,3,6))
        story.append(Paragraph(sec_title, sec_s))
        for item in items:
            story.append(Paragraph(f'• {item}', styles['body']))

def make_pdf(path):
    M = 18
    doc = SimpleDocTemplate(path, pagesize=A4,
                            leftMargin=M*mm, rightMargin=M*mm,
                            topMargin=M*mm, bottomMargin=M*mm)
    styles = make_styles()
    story  = []

    story.append(Paragraph(TITEL, styles['title']))
    story.append(Paragraph(UNTERTITEL, styles['sub']))
    story.append(HRFlowable(width='100%', thickness=1.5,
                             color=hx(COLORS['text']), spaceAfter=6))

    W_pt = A4[0]
    if LAYOUT == 'cards':
        build_cards_layout(story, styles, W_pt, {'left': M*mm, 'right': M*mm})
    else:
        build_single_layout(story, styles)

    # Tabellen
    for tbl_title, accent_col, header, rows in TABELLEN:
        story.append(Paragraph(tbl_title, styles['tbl_sec']))
        story.append(make_table(header, rows, accent_col))

    story.append(Paragraph(FUSSNOTE, styles['foot']))
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
    ('[ABSCHNITT 1 TITEL]', 'blue', [
        '[Stichpunkt 1]',
        '[Stichpunkt 2]',
    ]),
    ('[ABSCHNITT 2 TITEL]', 'green', [
        '[Stichpunkt 1]',
    ]),
]

TABELLEN = [
    ('[TABELLENTITEL]', 'blue',
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
    for sec_data in ABSCHNITTE:
        title, accent_col, items = sec_data[0], sec_data[1], sec_data[2]
        items_html = ''.join(f'<li>{i}</li>' for i in items)
        secs_html += f'''
        <div class="section">
          <h2>{title}</h2>
          <ul>{items_html}</ul>
        </div>'''

    tbls_html = ''
    for tbl_data in TABELLEN:
        tbl_title, accent_col, header, rows = tbl_data[0], tbl_data[1], tbl_data[2], tbl_data[3]
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
