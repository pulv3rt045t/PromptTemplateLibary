# TEMPLATE: Vergleichstabelle – Universalvorlage
# Datei: Template-Prompt-Comparison-v1.md
# Aufruf im Chat: "Vergleiche [A] vs [B]"
#
# ABLAUF: Siehe PROJEKT-INSTRUKTION (Abfrage 1 + 2 dort definiert)
#
# TEMPLATE-SPEZIFISCHE ZUSATZ-OPTIONEN (in Abfrage 2 ergänzen):
#   🔢 Anzahl Optionen: [ ] 2  [ ] 3  [ ] 4
#   ⭐ Empfehlung:      [ ] Ja (mit Begründung + Alternativ-Fall)  [ ] Nein
#
# ABFRAGE 1 ANGEPASST FÜR VERGLEICHE:
#   📌 Was wird verglichen? → max. 4 Optionen, Name je max. 14 Z.
#   📐 Vergleichskriterien? → Claude wählt oder eigene Eingabe
#   🎯 Entscheidungskontext? → wofür wird der Vergleich genutzt
#   🚫 Ausgeschlossene Aspekte?
#
# OPTIONEN ANWENDEN:
#   Druck/Web → C-Dict hell/dunkel (wie Standard)
#   2 Opt. → Zellinhalt max. 28 Z.  |  3 Opt. → max. 20 Z.  |  4 Opt. → max. 15 Z.
#   Empfehlung Ja → EMPFEHLUNG-Dict befüllen  |  Nein → EMPFEHLUNG = None
#   Erklär-Box Ja → ERKLAER_BOX befüllen      |  Nein → None
#
# FARBPALETTEN:
#   DRUCK:  page_bg:#ffffff  card_bg:#ffffff  card_border:#dddddd
#           val_text:#333333  footer_text:#999999  header_text:#111111
#           rule:#dddddd  bg:#f5f5f5
#   WEB:    page_bg:#0f0f0f  card_bg:#1a1a1a  card_border:#2e2e2e
#           val_text:#cccccc  footer_text:#555555  header_text:#ffffff
#   FARBEN: green:#1a6b00  blue:#004fa3  purple:#7a00b8
#           red:#b80000    orange:#b86000
#
# ZEICHENLIMITS:
#   Optionsname: max. 14 Z.  |  Kriterium: max. 20 Z.
#   Zellinhalt:  max. 28 Z. (2 Opt.) / 20 Z. (3 Opt.) / 15 Z. (4 Opt.)
#
# ENGINE NIEMALS VERÄNDERN – nur INHALT START/END Block ersetzen.
# ═══════════════════════════════════════════════════════════

```python
from reportlab.lib.pagesizes import A4
from reportlab.pdfgen import canvas
from reportlab.lib import colors

W, H = A4

# DRUCK (hell) – Standard:
C = {
    'green':  colors.HexColor('#1a6b00'),
    'blue':   colors.HexColor('#004fa3'),
    'purple': colors.HexColor('#7a00b8'),
    'red':    colors.HexColor('#b80000'),
    'orange': colors.HexColor('#b86000'),
    'black':  colors.HexColor('#111111'),
    'mid':    colors.HexColor('#333333'),
    'muted':  colors.HexColor('#666666'),
    'light':  colors.HexColor('#999999'),
    'rule':   colors.HexColor('#dddddd'),
    'bg':     colors.HexColor('#f5f5f5'),
    'white':  colors.white,
    'page_bg':     colors.white,
    'card_bg':     colors.white,
    'card_border': colors.HexColor('#dddddd'),
    'val_text':    colors.HexColor('#333333'),
    'footer_text': colors.HexColor('#999999'),
    'header_text': colors.HexColor('#111111'),
}
# WEB/BILDSCHIRM (dunkel) – einkommentieren wenn Modus=Web:
# C = {
#     'green':  colors.HexColor('#1a6b00'),
#     'blue':   colors.HexColor('#004fa3'),
#     'purple': colors.HexColor('#7a00b8'),
#     'red':    colors.HexColor('#b80000'),
#     'orange': colors.HexColor('#b86000'),
#     'black':  colors.HexColor('#111111'),
#     'mid':    colors.HexColor('#333333'),
#     'muted':  colors.HexColor('#666666'),
#     'light':  colors.HexColor('#999999'),
#     'rule':   colors.HexColor('#2e2e2e'),
#     'bg':     colors.HexColor('#252525'),
#     'white':  colors.white,
#     'page_bg':     colors.HexColor('#0f0f0f'),
#     'card_bg':     colors.HexColor('#1a1a1a'),
#     'card_border': colors.HexColor('#2e2e2e'),
#     'val_text':    colors.HexColor('#cccccc'),
#     'footer_text': colors.HexColor('#555555'),
#     'header_text': colors.HexColor('#ffffff'),
# }

# ═══════════════════════════════════════════════
# ── INHALT START ── (NUR DIESEN BLOCK ERSETZEN)
# ═══════════════════════════════════════════════

TITEL      = '[OPTION A] vs [OPTION B] – VERGLEICH'
UNTERTITEL = '[Kontext / Entscheidungshilfe  ·  Quelle/Datum]'
TIPP       = 'Tipp: [Einprägsamer Entscheidungs-Merksatz – max. 80 Zeichen]'

# Farbe für Spaltenheader der Optionen: 'green'|'blue'|'purple'|'red'|'orange'
HEADER_FARBE = 'blue'

# Die verglichenen Optionen (2–4 Einträge, Name max. 14 Zeichen)
OPTIONEN = [
    '[Option A]',
    '[Option B]',
    # '[Option C]',  # optional – auskommentieren wenn nur 2 Optionen
    # '[Option D]',  # optional
]

# Vergleichskriterien: (Kriterium, [Wert Option A, Wert Option B, ...])
# Kriterium max. 20 Z. | Wert max. 28 Z. (2 Opt.) / 20 Z. (3 Opt.) / 15 Z. (4 Opt.)
# Kompakt: 8–10 Kriterien | Ausführlich: 14–18 Kriterien
# Tipp: Werte parallel strukturieren (alle Ja/Nein, oder alle Kurzphrasen)
KRITERIEN = [
    ('[Kriterium 1]',  ['[Wert A]',  '[Wert B]']),
    ('[Kriterium 2]',  ['[Wert A]',  '[Wert B]']),
    ('[Kriterium 3]',  ['[Wert A]',  '[Wert B]']),
    ('[Kriterium 4]',  ['[Wert A]',  '[Wert B]']),
    ('[Kriterium 5]',  ['[Wert A]',  '[Wert B]']),
    ('[Kriterium 6]',  ['[Wert A]',  '[Wert B]']),
    ('[Kriterium 7]',  ['[Wert A]',  '[Wert B]']),
    ('[Kriterium 8]',  ['[Wert A]',  '[Wert B]']),
    # Kompakt: bis hier. Ausführlich: weiter bis 18 Kriterien.
]

# EMPFEHLUNG (None = nicht anzeigen)
EMPFEHLUNG = None
# EMPFEHLUNG = {
#     'titel':  '■ EMPFEHLUNG',
#     'farbe':  'green',   # Akzentfarbe der Empfehlungszeile
#     'wahl':   '[Option X]',
#     'grund':  '[1 Satz: Hauptgrund für die Empfehlung]',
#     'wenn':   '[Option Y] wenn: [Alternativer Anwendungsfall]',
# }

# ERKLÄR-BOX (None = nicht anzeigen, empfohlen für Einsteiger)
ERKLAER_BOX = None
# ERKLAER_BOX = ('[THEMA] – HINTERGRUND & KONTEXT', 'blue', [
#     '[Was wird hier verglichen? Wozu dient dieser Vergleich?]',
#     '[In welchem Kontext / welcher Entscheidung ist das relevant?]',
#     '[Was ist das Wichtigste bei dieser Entscheidung?]',
# ])

FUSSNOTE = '[Quelle / Datum / Version]'

# ═══════════════════════════════════════════════
# ── INHALT END ──
# ═══════════════════════════════════════════════


# ── ENGINE (NICHT VERÄNDERN) ────────────────────────────────

def wrap_text(cv, text, font, size, max_width):
    words = text.split(' ')
    lines, line = [], ''
    for word in words:
        test = (line + ' ' + word).strip()
        if cv.stringWidth(test, font, size) <= max_width:
            line = test
        else:
            if line: lines.append(line)
            line = word
    if line: lines.append(line)
    return lines

def draw_header(cv):
    M = 18
    hdr_y = H - M - 20
    xc = M
    for pi, word in enumerate(TITEL.split(' ')):
        font = 'Helvetica' if pi == 1 else 'Helvetica-Bold'
        col  = C['muted'] if pi == 1 else C['header_text']
        cv.setFont(font, 16); cv.setFillColor(col)
        cv.drawString(xc, hdr_y, word)
        xc += cv.stringWidth(word, font, 16) + 5
    cv.setFont('Helvetica', 6.5); cv.setFillColor(C['footer_text'])
    cv.drawRightString(W - M, hdr_y, UNTERTITEL)
    cv.setStrokeColor(C['header_text']); cv.setLineWidth(1.5)
    rule_y = hdr_y - 8
    cv.line(M, rule_y, W - M, rule_y)
    return rule_y

def draw_erklaer_box(cv, x, y, w, h, title, accent, lines):
    bar_h = 16
    cv.setFillColor(C['card_bg']); cv.setStrokeColor(C['card_border']); cv.setLineWidth(0.6)
    cv.roundRect(x, y, w, h, 4, stroke=1, fill=1)
    cv.setFillColor(C[accent])
    cv.roundRect(x, y + h - bar_h, w, bar_h, 4, stroke=0, fill=1)
    cv.rect(x, y + h - bar_h, w, bar_h // 2, stroke=0, fill=1)
    cv.setFont('Helvetica-Bold', 7); cv.setFillColor(C['white'])
    cv.drawString(x + 8, y + h - bar_h + 5, title)
    body_h = h - bar_h
    font_size = 7.5; line_h = font_size * 1.6
    pad_x = x + 9; pad_max = w - 18
    n = len(lines); row_h = body_h / max(n, 1)
    for i, line in enumerate(lines):
        row_mid_y = y + body_h - (i + 0.5) * row_h
        wrapped = wrap_text(cv, line, 'Helvetica', font_size, pad_max)
        text_block_h = (len(wrapped) - 1) * line_h + font_size
        top_baseline = row_mid_y + text_block_h / 2 - font_size * 0.82
        for li, ln in enumerate(wrapped):
            cv.setFont('Helvetica', font_size); cv.setFillColor(C['val_text'])
            cv.drawString(pad_x, top_baseline - li * line_h, ln)
        if i < n - 1:
            div_y = y + body_h - (i + 1) * row_h
            cv.setStrokeColor(C['rule']); cv.setLineWidth(0.4)
            cv.line(pad_x, div_y, x + w - 9, div_y)

def draw_comparison_table(cv, x, y, w, h):
    n_opts   = len(OPTIONEN)
    n_rows   = len(KRITERIEN)
    bar_h    = 16        # Titelbalken
    pad      = 7
    fs_head  = 7.5
    fs_body  = 7.0
    row_h    = (h - bar_h - pad) / (n_rows + 1)  # +1 für Headerzeile

    # Spaltenbreiten: Kriterium-Spalte 30%, Rest gleich verteilt
    crit_w   = w * 0.28
    opt_w    = (w - crit_w) / n_opts

    # Titelbalken
    cv.setFillColor(C[HEADER_FARBE])
    cv.roundRect(x, y + h - bar_h, w, bar_h, 4, stroke=0, fill=1)
    cv.rect(x, y + h - bar_h, w, bar_h // 2, stroke=0, fill=1)
    cv.setFont('Helvetica-Bold', 7); cv.setFillColor(C['white'])
    cv.drawString(x + 8, y + h - bar_h + 5, TITEL)

    # Rahmen gesamt
    cv.setFillColor(C['card_bg']); cv.setStrokeColor(C['card_border']); cv.setLineWidth(0.6)
    cv.roundRect(x, y, w, h - bar_h, 4, stroke=1, fill=1)

    # Optionen-Header-Zeile
    header_y = y + h - bar_h - row_h
    cv.setFillColor(C[HEADER_FARBE])
    cv.rect(x, header_y, w, row_h, stroke=0, fill=1)

    # Kriterium-Spalte Header
    cv.setFont('Helvetica-Bold', fs_head); cv.setFillColor(C['white'])
    cv.drawString(x + 6, header_y + row_h * 0.35, 'Kriterium')

    # Optionen-Namen in Header
    for i, opt in enumerate(OPTIONEN):
        ox = x + crit_w + i * opt_w
        ow = opt_w - 4
        opt_lines = wrap_text(cv, opt, 'Helvetica-Bold', fs_head, ow)
        for li, ol in enumerate(opt_lines):
            cv.drawString(ox + 5, header_y + row_h * 0.55 - li * (fs_head * 1.2), ol)

    # Trennlinien Spalten im Header
    cv.setStrokeColor(colors.HexColor('#ffffff40')); cv.setLineWidth(0.4)
    for i in range(1, n_opts + 1):
        lx = x + crit_w + (i - 1) * opt_w
        if i > 0:
            cv.line(lx, header_y, lx, header_y + row_h)

    # Datenzeilen
    for ri, (krit, werte) in enumerate(KRITERIEN):
        ry = y + h - bar_h - row_h * (ri + 2)

        # Zebra-Hintergrund
        if ri % 2 == 0:
            cv.setFillColor(C['bg'])
            cv.rect(x, ry, w, row_h, stroke=0, fill=1)

        # Kriterium
        cv.setFont('Helvetica-Bold', fs_body); cv.setFillColor(C[HEADER_FARBE])
        krit_lines = wrap_text(cv, krit, 'Helvetica-Bold', fs_body, crit_w - 10)
        for li, kl in enumerate(krit_lines):
            cv.drawString(x + 6, ry + row_h * 0.62 - li * (fs_body * 1.3), kl)

        # Trennlinie Kriterium-Spalte
        cv.setStrokeColor(C['rule']); cv.setLineWidth(0.4)
        cv.line(x + crit_w, ry, x + crit_w, ry + row_h)

        # Werte
        for ci, wert in enumerate(werte[:n_opts]):
            ox = x + crit_w + ci * opt_w
            ow = opt_w - 8
            cv.setFont('Helvetica', fs_body); cv.setFillColor(C['val_text'])
            wert_lines = wrap_text(cv, wert, 'Helvetica', fs_body, ow)
            for li, wl in enumerate(wert_lines):
                cv.drawString(ox + 5, ry + row_h * 0.62 - li * (fs_body * 1.3), wl)
            # Trennlinie zwischen Optionsspalten
            if ci < n_opts - 1:
                cv.setStrokeColor(C['rule']); cv.setLineWidth(0.3)
                cv.line(ox + opt_w, ry, ox + opt_w, ry + row_h)

        # Horizontale Trennlinie
        cv.setStrokeColor(C['rule']); cv.setLineWidth(0.4)
        cv.line(x + 4, ry, x + w - 4, ry)

def draw_empfehlung(cv, x, y, w, h):
    if not EMPFEHLUNG:
        return
    bar_h = 16
    cv.setFillColor(C[EMPFEHLUNG['farbe']])
    cv.roundRect(x, y + h - bar_h, w, bar_h, 4, stroke=0, fill=1)
    cv.rect(x, y + h - bar_h, w, bar_h // 2, stroke=0, fill=1)
    cv.setFont('Helvetica-Bold', 7); cv.setFillColor(C['white'])
    cv.drawString(x + 8, y + h - bar_h + 5, EMPFEHLUNG['titel'])

    cv.setFillColor(C['card_bg']); cv.setStrokeColor(C['card_border']); cv.setLineWidth(0.6)
    cv.roundRect(x, y, w, h - bar_h, 4, stroke=1, fill=1)

    body_h = h - bar_h
    pad_x = x + 9; pad_max = w - 18; fs = 7.5; lh = fs * 1.5

    # Wahl
    wahl_text = f'→ {EMPFEHLUNG["wahl"]}'
    cv.setFont('Helvetica-Bold', fs + 0.5); cv.setFillColor(C[EMPFEHLUNG['farbe']])
    cv.drawString(pad_x, y + body_h - 14, wahl_text)

    cv.setStrokeColor(C['rule']); cv.setLineWidth(0.4)
    cv.line(pad_x, y + body_h - 18, x + w - 9, y + body_h - 18)

    # Grund
    grund_lines = wrap_text(cv, EMPFEHLUNG['grund'], 'Helvetica', fs, pad_max)
    for li, gl in enumerate(grund_lines):
        cv.setFont('Helvetica', fs); cv.setFillColor(C['val_text'])
        cv.drawString(pad_x, y + body_h - 26 - li * lh, gl)

    # Wenn-Zeile
    wenn_lines = wrap_text(cv, EMPFEHLUNG['wenn'], 'Helvetica-Oblique', fs - 0.5, pad_max)
    offset = 26 + len(grund_lines) * lh + 6
    for li, wl in enumerate(wenn_lines):
        cv.setFont('Helvetica-Oblique', fs - 0.5); cv.setFillColor(C['muted'])
        cv.drawString(pad_x, y + body_h - offset - li * lh, wl)

def make_pdf(path):
    cv = canvas.Canvas(path, pagesize=A4)
    cv.setTitle(TITEL)
    M = 18; GAP = 5; FOOTER_H = 18

    cv.setFillColor(C['page_bg']); cv.rect(0, 0, W, H, stroke=0, fill=1)
    rule_y = draw_header(cv)

    content_top  = rule_y - GAP
    content_h    = content_top - (M + FOOTER_H)
    usable_w     = W - 2 * M

    # Erklaer-Box: oben rechts (1/3 Breite) wenn aktiv
    if ERKLAER_BOX:
        erkl_w  = usable_w / 3
        erkl_h  = content_h * 0.14
        erkl_x  = M + usable_w - erkl_w
        erkl_y  = content_top - erkl_h
        draw_erklaer_box(cv, erkl_x, erkl_y, erkl_w, erkl_h, *ERKLAER_BOX)
        tbl_w   = usable_w - erkl_w - GAP
        tbl_x   = M
    else:
        tbl_w   = usable_w
        tbl_x   = M

    # Empfehlung: unten (wenn aktiv)
    if EMPFEHLUNG:
        emp_h   = content_h * 0.13
        emp_y   = M + FOOTER_H
        draw_empfehlung(cv, M, emp_y, usable_w, emp_h)
        tbl_h   = content_h - emp_h - GAP
    else:
        tbl_h   = content_h

    tbl_y = content_top - tbl_h
    draw_comparison_table(cv, tbl_x, tbl_y, tbl_w, tbl_h)

    # Footer
    fy = M + FOOTER_H - 4
    cv.setStrokeColor(C['rule']); cv.setLineWidth(0.5)
    cv.line(M, fy, W - M, fy)
    cv.setFont('Helvetica', 6.5); cv.setFillColor(C['footer_text'])
    cv.drawString(M, fy - 8, TITEL)
    cv.setFont('Helvetica-Bold', 6.5); cv.setFillColor(C['muted'])
    cv.drawCentredString(W / 2, fy - 8, TIPP)
    cv.setFont('Helvetica', 6.5); cv.setFillColor(C['footer_text'])
    cv.drawRightString(W - M, fy - 8, FUSSNOTE)
    cv.save()
    print(f"Done → {path}")

make_pdf('/home/claude/output.pdf')
```
