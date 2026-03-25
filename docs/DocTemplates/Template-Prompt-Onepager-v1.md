# TEMPLATE: One-Pager – Universalvorlage
# Datei: Template-Prompt-Onepager-v1.md
# Aufruf im Chat: "Onepager zu [THEMA]"
#
# ABLAUF: Siehe PROJEKT-INSTRUKTION (Abfrage 1 + 2 dort definiert)
#
# TEMPLATE-SPEZIFISCHE ZUSATZ-OPTIONEN (in Abfrage 2 ergänzen):
#   🎨 Stil:      [ ] Sachlich/Professionell  [ ] Modern/Visuell
#   📊 Struktur:  [ ] Standard (Zusammenfassung + Blöcke + Nächste Schritte)
#                 [ ] Pitch    (Problem → Lösung → Nutzen → CTA)
#                 [ ] Status   (Überblick → Erledigtes → Offenes → Risiken)
#
# ABFRAGE 1 ANGEPASST FÜR ONE-PAGER:
#   📌 Titel?  🎯 Zweck? (Entscheidungsvorlage / Pitch / Status / Einführung)
#   👥 Zielgruppe / Leser?  🚫 Was soll NICHT enthalten sein?
#
# OPTIONEN ANWENDEN:
#   Sachlich → AKZENT_FARBE = 'blue'     |  Modern → Farbe nach Thema
#   Standard → STRUKTUR = 'standard'     |  SCHRITTE_TITEL = 'NÄCHSTE SCHRITTE'
#   Pitch    → STRUKTUR = 'pitch'        |  SCHRITTE_TITEL = 'CALL TO ACTION'
#   Status   → STRUKTUR = 'status'       |  SCHRITTE_TITEL = 'NEXT STEPS'
#   Erklär-Box Ja → ERKLAER_BOX befüllen |  Nein → None
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
#   Stichpunkt: max. 65 Z. (1-spaltig) / 45 Z. (2-spaltig)
#   Block-Titel: max. 22 Z.  |  max. 4 BLOECKE  |  max. 4 NAECHSTE_SCHRITTE
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

TITEL        = '[THEMA / PROJEKTNAME]'
UNTERTITEL   = '[Zweck · Zielgruppe · Datum]'
AKZENT_FARBE = 'blue'   # 'green'|'blue'|'purple'|'red'|'orange'
STRUKTUR     = 'standard'  # 'standard' | 'pitch' | 'status'
TIPP         = '[Kernbotschaft oder Call-to-Action – max. 80 Zeichen]'

# ZUSAMMENFASSUNG / LEAD (1–3 Sätze, max. ~180 Zeichen gesamt)
ZUSAMMENFASSUNG = '[Ein bis drei Sätze die den Kern auf den Punkt bringen. Was ist das Wichtigste?]'

# ERKLÄR-BOX (None = nicht anzeigen)
ERKLAER_BOX = None
# ERKLAER_BOX = ('[HINTERGRUND & KONTEXT]', 'blue', [
#     '[Was ist der Hintergrund dieses Dokuments?]',
#     '[Für wen ist es gedacht und warum ist es relevant?]',
# ])

# ── STRUKTUR: 'standard' ──────────────────────
# Inhaltsblöcke: Liste von (Titel, Akzentfarbe, [Stichpunkte])
# Titel max. 22 Z. | Stichpunkt max. 65 Z. (Vollbreite) / 45 Z. (2 Blöcke nebeneinander)
# 2–4 Blöcke empfohlen, je 3–5 Stichpunkte
BLOECKE = [
    ('[BLOCK 1 TITEL]', 'blue', [
        '[Stichpunkt 1 – prägnant, max. 65 Zeichen]',
        '[Stichpunkt 2]',
        '[Stichpunkt 3]',
    ]),
    ('[BLOCK 2 TITEL]', 'green', [
        '[Stichpunkt 1]',
        '[Stichpunkt 2]',
        '[Stichpunkt 3]',
    ]),
    ('[BLOCK 3 TITEL]', 'purple', [
        '[Stichpunkt 1]',
        '[Stichpunkt 2]',
    ]),
    ('[BLOCK 4 TITEL]', 'orange', [
        '[Stichpunkt 1]',
        '[Stichpunkt 2]',
    ]),
]

# NÄCHSTE SCHRITTE / CALL-TO-ACTION (max. 4 Einträge)
NAECHSTE_SCHRITTE = [
    '[Schritt 1 – konkret, umsetzbar, max. 55 Zeichen]',
    '[Schritt 2]',
    '[Schritt 3]',
    # '[Schritt 4]',  # optional
]
SCHRITTE_TITEL = 'NÄCHSTE SCHRITTE'

# ── STRUKTUR: 'pitch' – alternativ ────────────
# Wird verwendet wenn STRUKTUR = 'pitch'
# BLOECKE dann: Problem / Lösung / Nutzen / (Belege optional)
# NAECHSTE_SCHRITTE dann: Call-to-Action Zeile(n)
# SCHRITTE_TITEL = 'CALL TO ACTION'

# ── STRUKTUR: 'status' – alternativ ───────────
# Wird verwendet wenn STRUKTUR = 'status'
# BLOECKE dann: Überblick / Erledigtes / Offenes / Risiken
# NAECHSTE_SCHRITTE dann: Next Steps mit Verantwortlichen
# SCHRITTE_TITEL = 'NEXT STEPS'

FUSSNOTE = '[Autor · Datum · Version · Kontakt]'

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

def draw_card(cv, x, y, w, h, title, accent, items, fs_body=8.0):
    bar_h = 15
    cv.setFillColor(C['card_bg']); cv.setStrokeColor(C['card_border']); cv.setLineWidth(0.6)
    cv.roundRect(x, y, w, h, 4, stroke=1, fill=1)
    cv.setFillColor(C[accent])
    cv.roundRect(x, y + h - bar_h, w, bar_h, 4, stroke=0, fill=1)
    cv.rect(x, y + h - bar_h, w, bar_h // 2, stroke=0, fill=1)
    cv.setFont('Helvetica-Bold', 7); cv.setFillColor(C['white'])
    cv.drawString(x + 7, y + h - bar_h + 4, title)

    body_h   = h - bar_h
    pad_x    = x + 9
    pad_max  = w - 16
    lh       = fs_body * 1.55
    bullet_x = pad_x
    text_x   = pad_x + 8

    # Gleichmäßige vertikale Verteilung
    n = len(items)
    row_h = body_h / max(n, 1)

    for i, item in enumerate(items):
        row_mid_y = y + body_h - (i + 0.5) * row_h
        item_lines = wrap_text(cv, item, 'Helvetica', fs_body, pad_max - 8)
        text_block_h = (len(item_lines) - 1) * lh + fs_body
        top_baseline = row_mid_y + text_block_h / 2 - fs_body * 0.82

        # Bullet
        cv.setFillColor(C[accent])
        cv.circle(bullet_x + 2, top_baseline - fs_body * 0.1 + fs_body * 0.3, 1.8, stroke=0, fill=1)

        for li, il in enumerate(item_lines):
            cv.setFont('Helvetica', fs_body); cv.setFillColor(C['val_text'])
            cv.drawString(text_x, top_baseline - li * lh, il)

        if i < n - 1:
            div_y = y + body_h - (i + 1) * row_h
            cv.setStrokeColor(C['rule']); cv.setLineWidth(0.35)
            cv.line(pad_x, div_y, x + w - 7, div_y)

def draw_summary(cv, x, y, w, h):
    cv.setFillColor(C[AKZENT_FARBE])
    cv.roundRect(x, y + h - 14, w, 14, 4, stroke=0, fill=1)
    cv.rect(x, y + h - 14, w, 7, stroke=0, fill=1)
    cv.setFont('Helvetica-Bold', 7); cv.setFillColor(C['white'])
    cv.drawString(x + 7, y + h - 14 + 4, 'ZUSAMMENFASSUNG')
    cv.setFillColor(C['bg']); cv.setStrokeColor(C['card_border']); cv.setLineWidth(0.6)
    cv.roundRect(x, y, w, h - 14, 4, stroke=1, fill=1)
    body_h = h - 14
    fs = 8.5
    lines = wrap_text(cv, ZUSAMMENFASSUNG, 'Helvetica', fs, w - 16)
    lh = fs * 1.6
    text_block_h = (len(lines) - 1) * lh + fs
    start_y = y + (body_h + text_block_h) / 2 - fs * 0.82
    for li, ln in enumerate(lines):
        cv.setFont('Helvetica', fs); cv.setFillColor(C['val_text'])
        cv.drawString(x + 9, start_y - li * lh, ln)

def draw_erklaer_box(cv, x, y, w, h, title, accent, lines):
    bar_h = 15
    cv.setFillColor(C['card_bg']); cv.setStrokeColor(C['card_border']); cv.setLineWidth(0.6)
    cv.roundRect(x, y, w, h, 4, stroke=1, fill=1)
    cv.setFillColor(C[accent])
    cv.roundRect(x, y + h - bar_h, w, bar_h, 4, stroke=0, fill=1)
    cv.rect(x, y + h - bar_h, w, bar_h // 2, stroke=0, fill=1)
    cv.setFont('Helvetica-Bold', 7); cv.setFillColor(C['white'])
    cv.drawString(x + 7, y + h - bar_h + 4, title)
    body_h = h - bar_h; fs = 7.5; lh = fs * 1.6
    pad_x = x + 9; pad_max = w - 18
    n = len(lines); row_h = body_h / max(n, 1)
    for i, line in enumerate(lines):
        row_mid_y = y + body_h - (i + 0.5) * row_h
        wrapped = wrap_text(cv, line, 'Helvetica', fs, pad_max)
        text_block_h = (len(wrapped) - 1) * lh + fs
        top_baseline = row_mid_y + text_block_h / 2 - fs * 0.82
        for li, ln in enumerate(wrapped):
            cv.setFont('Helvetica', fs); cv.setFillColor(C['val_text'])
            cv.drawString(pad_x, top_baseline - li * lh, ln)
        if i < n - 1:
            div_y = y + body_h - (i + 1) * row_h
            cv.setStrokeColor(C['rule']); cv.setLineWidth(0.4)
            cv.line(pad_x, div_y, x + w - 9, div_y)

def draw_naechste_schritte(cv, x, y, w, h):
    bar_h = 15
    cv.setFillColor(C[AKZENT_FARBE])
    cv.roundRect(x, y + h - bar_h, w, bar_h, 4, stroke=0, fill=1)
    cv.rect(x, y + h - bar_h, w, bar_h // 2, stroke=0, fill=1)
    cv.setFont('Helvetica-Bold', 7); cv.setFillColor(C['white'])
    cv.drawString(x + 7, y + h - bar_h + 4, SCHRITTE_TITEL)
    cv.setFillColor(C['card_bg']); cv.setStrokeColor(C['card_border']); cv.setLineWidth(0.6)
    cv.roundRect(x, y, w, h - bar_h, 4, stroke=1, fill=1)

    body_h = h - bar_h; fs = 8.0; lh = fs * 1.55
    n = len(NAECHSTE_SCHRITTE); row_h = body_h / max(n, 1)
    pad_max = w - 28

    for i, step in enumerate(NAECHSTE_SCHRITTE):
        row_mid_y = y + body_h - (i + 0.5) * row_h
        step_lines = wrap_text(cv, step, 'Helvetica', fs, pad_max)
        text_block_h = (len(step_lines) - 1) * lh + fs
        top_baseline = row_mid_y + text_block_h / 2 - fs * 0.82

        # Nummerierung
        num = str(i + 1)
        num_w = 14
        cv.setFillColor(C[AKZENT_FARBE])
        cv.circle(x + 13, top_baseline - fs * 0.1 + fs * 0.3, 5.5, stroke=0, fill=1)
        cv.setFont('Helvetica-Bold', 6); cv.setFillColor(C['white'])
        cv.drawCentredString(x + 13, top_baseline - fs * 0.12 + fs * 0.2, num)

        for li, sl in enumerate(step_lines):
            cv.setFont('Helvetica', fs); cv.setFillColor(C['val_text'])
            cv.drawString(x + num_w + 9, top_baseline - li * lh, sl)

        if i < n - 1:
            div_y = y + body_h - (i + 1) * row_h
            cv.setStrokeColor(C['rule']); cv.setLineWidth(0.35)
            cv.line(x + 7, div_y, x + w - 7, div_y)

def make_pdf(path):
    cv = canvas.Canvas(path, pagesize=A4)
    cv.setTitle(TITEL)
    M = 18; GAP = 6; FOOTER_H = 18

    cv.setFillColor(C['page_bg']); cv.rect(0, 0, W, H, stroke=0, fill=1)

    # Header
    hdr_y = H - M - 22
    cv.setFont('Helvetica-Bold', 20); cv.setFillColor(C['header_text'])
    cv.drawString(M, hdr_y, TITEL)
    cv.setFont('Helvetica', 7.5); cv.setFillColor(C['footer_text'])
    cv.drawRightString(W - M, hdr_y, UNTERTITEL)

    # Akzentbalken unter Titel
    bar_y = hdr_y - 6
    cv.setFillColor(C[AKZENT_FARBE])
    cv.rect(M, bar_y, W - 2 * M, 2.5, stroke=0, fill=1)

    content_top = bar_y - GAP
    content_h   = content_top - (M + FOOTER_H)
    usable_w    = W - 2 * M

    # Höhenverteilung
    summ_h   = content_h * 0.12
    steps_h  = content_h * 0.18
    erkl_h   = content_h * 0.13 if ERKLAER_BOX else 0
    erkl_gap = GAP if ERKLAER_BOX else 0
    blocks_h = content_h - summ_h - steps_h - erkl_h - 3 * GAP - erkl_gap

    # Zusammenfassung (oben, volle Breite)
    summ_y = content_top - summ_h
    draw_summary(cv, M, summ_y, usable_w, summ_h)

    # Erklär-Box (unter Zusammenfassung, falls aktiv)
    if ERKLAER_BOX:
        erkl_y = summ_y - GAP - erkl_h
        draw_erklaer_box(cv, M, erkl_y, usable_w, erkl_h, *ERKLAER_BOX)
        blocks_top = erkl_y - GAP
    else:
        blocks_top = summ_y - GAP

    # Inhaltsblöcke (2-spaltig wenn 3–4 Blöcke, 1-spaltig wenn 1–2)
    n_blocks = len(BLOECKE)
    if n_blocks >= 3:
        col_w  = (usable_w - GAP) / 2
        for i, (btitel, bfarbe, bitems) in enumerate(BLOECKE):
            bx = M + (i % 2) * (col_w + GAP)
            n_rows = (n_blocks + 1) // 2
            row_idx = i // 2
            bh = (blocks_h - (n_rows - 1) * GAP) / n_rows
            by = blocks_top - row_idx * (bh + GAP) - bh
            draw_card(cv, bx, by, col_w, bh, btitel, bfarbe, bitems)
    else:
        bh = (blocks_h - (n_blocks - 1) * GAP) / max(n_blocks, 1)
        for i, (btitel, bfarbe, bitems) in enumerate(BLOECKE):
            by = blocks_top - i * (bh + GAP) - bh
            draw_card(cv, M, by, usable_w, bh, btitel, bfarbe, bitems)

    # Nächste Schritte (unten, volle Breite)
    steps_y = M + FOOTER_H
    draw_naechste_schritte(cv, M, steps_y, usable_w, steps_h)

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
