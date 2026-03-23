# TEMPLATE: Cheat Sheet · Druck · Experte · Ausführlich
# Trigger: [THEMA] - Web-Experte-Ausfuehrlich
#
# ANWEISUNG AN CLAUDE:
# 1. Kopiere den GESAMTEN Python-Code unverändert
# 2. Ersetze NUR den Block zwischen ── INHALT START ── und ── INHALT END ──
# 3. Führe das Script aus und liefere die PDF
# 4. Verändere NIEMALS die Engine-Funktionen (draw_rows, wrap_text, card_bg, etc.)

# MODUS: DRUCK | ZIELGRUPPE: EXPERTE | UMFANG: AUSFÜHRLICH
# CODE-BOX: JA
# Karten 1+2: 10–12 Einträge | Karten 3+4+5: 8–10 Einträge
# Fachbegriffe erlaubt, keine Grundlagen-Erklärungen

```python
from reportlab.lib.pagesizes import A4
from reportlab.pdfgen import canvas
from reportlab.lib import colors

W, H = A4

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
    'rule':   colors.HexColor('#2e2e2e'),
    'bg':     colors.HexColor('#252525'),
    'white':  colors.white,
    'page_bg':     colors.HexColor('#0f0f0f'),
    'card_bg':     colors.HexColor('#1a1a1a'),
    'card_border': colors.HexColor('#2e2e2e'),
    'val_text':    colors.HexColor('#cccccc'),
    'footer_text': colors.HexColor('#555555'),
    'header_text': colors.HexColor('#ffffff'),
}

# ═══════════════════════════════════════════════
# ── INHALT START ── (NUR DIESEN BLOCK ERSETZEN)
# ═══════════════════════════════════════════════

TITEL      = '[THEMA IN GROSSBUCHSTABEN] CHEAT SHEET'
UNTERTITEL = '[Kurzbeschreibung  ·  Quelle/Website]'
TIPP       = 'Tipp: [Themenspezifischer Experten-Merksatz]'

SECTIONS = [
    ('[KARTE 1 TITEL]', 'green', [
        ('[Keyword 1]',  '[Beschreibung 1]'),
        ('[Keyword 2]',  '[Beschreibung 2]'),
        # ... 10–12 Einträge, Keyword max. 18 Z., Beschreibung max. 35 Z.
    ]),
    ('[KARTE 2 TITEL]', 'blue', [
        ('[Keyword 1]',  '[Beschreibung 1]'),
        # ... 10–12 Einträge
    ]),
    ('[KARTE 3 TITEL]', 'purple', [
        ('[Keyword 1]',  '[Beschreibung 1]'),
        # ... 8–10 Einträge
    ]),
    ('[KARTE 4 TITEL]', 'red', [
        ('[Keyword 1]',  '[Beschreibung 1]'),
        # ... 8–10 Einträge
    ]),
    ('[KARTE 5 TITEL]', 'orange', [
        ('[Keyword 1]',  '[Beschreibung 1]'),
        # ... 6–8 Einträge
    ]),
]

MODIFIERS = [
    ('[Label 1]',  '[Beschreibung 1]',  'green'),
    ('[Label 2]',  '[Beschreibung 2]',  'blue'),
    ('[Label 3]',  '[Beschreibung 3]',  'purple'),
    ('[Label 4]',  '[Beschreibung 4]',  'red'),
    ('[Label 5]',  '[Beschreibung 5]',  'orange'),
    ('[Label 6]',  '[Beschreibung 6]',  'green'),
    ('[Label 7]',  '[Beschreibung 7]',  'blue'),
    ('[Label 8]',  '[Beschreibung 8]',  'purple'),
    ('[Label 9]',  '[Beschreibung 9]',  'red'),
    ('[Label 10]', '[Beschreibung 10]', 'orange'),
    # GENAU 10 Einträge, Label max. 14 Z., Beschreibung max. 22 Z.
]

TIPS = [
    ('[Tipp 1]', '[Handlungsempfehlung 1]'),
    ('[Tipp 2]', '[Handlungsempfehlung 2]'),
    ('[Tipp 3]', '[Handlungsempfehlung 3]'),
    ('[Tipp 4]', '[Handlungsempfehlung 4]'),
    ('[Tipp 5]', '[Handlungsempfehlung 5]'),
    ('[Tipp 6]', '[Handlungsempfehlung 6]'),
    # GENAU 6 Einträge
]

TIPS_TITEL = 'BEST PRACTICES'

# CODE-BOX: Titel, Titelbalken-Farbe, Code-Zeilen (max. 16)
CODE_BOX = ('[PRAXISBEISPIEL – TYPISCHER USE CASE]', 'blue', [
    '# [Schritt 1 Kommentar]',
    '[code zeile 1]',
    '',
    '# [Schritt 2 Kommentar]',
    '[code zeile 2]',
    # ... max. 16 Zeilen
])

FORMEL_LABEL   = None  # Nicht verwendet wenn CODE_BOX gesetzt
FORMEL_TEILE   = []
FORMEL_BEISPIEL = ''

# ═══════════════════════════════════════════════
# ── INHALT END ──
# ═══════════════════════════════════════════════


# ── ENGINE (NICHT VERÄNDERN) ──

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

def card_bg(cv, x, y, w, h, accent_color, title, radius=4):
    bar_h = 16
    cv.setFillColor(C['card_bg'])
    cv.setStrokeColor(C['card_border'])
    cv.setLineWidth(0.6)
    cv.roundRect(x, y, w, h, radius, stroke=1, fill=1)
    cv.setFillColor(C[accent_color])
    cv.roundRect(x, y + h - bar_h, w, bar_h, radius, stroke=0, fill=1)
    cv.rect(x, y + h - bar_h, w, bar_h // 2, stroke=0, fill=1)
    cv.setFont('Helvetica-Bold', 7)
    cv.setFillColor(C['white'])
    cv.drawString(x + 8, y + h - bar_h + 5, title)

def draw_rows(cv, x, y, w, h, rows, key_color, key_ratio=0.40):
    font_size = 7.5
    line_h    = font_size * 1.5
    key_x     = x + 7
    val_x     = x + w * key_ratio
    key_max   = w * key_ratio - 12
    val_max   = w * (1 - key_ratio) - 10
    wrapped = []
    for key, val in rows:
        k_lines = wrap_text(cv, key, 'Helvetica-Bold', font_size, key_max)
        v_lines = wrap_text(cv, val, 'Helvetica',      font_size, val_max)
        wrapped.append((k_lines, v_lines, max(len(k_lines), len(v_lines))))
    n     = len(wrapped)
    row_h = h / n
    for i, (k_lines, v_lines, n_lines) in enumerate(wrapped):
        row_mid_y    = y + h - (i + 0.5) * row_h
        text_block_h = (n_lines - 1) * line_h + font_size
        top_baseline = row_mid_y + text_block_h / 2 - font_size * 0.82
        for li, kl in enumerate(k_lines):
            cv.setFont('Helvetica-Bold', font_size)
            cv.setFillColor(C[key_color])
            cv.drawString(key_x, top_baseline - li * line_h, kl)
        for li, vl in enumerate(v_lines):
            cv.setFont('Helvetica', font_size)
            cv.setFillColor(C['val_text'])
            cv.drawString(val_x, top_baseline - li * line_h, vl)
        if i < n - 1:
            div_y = y + h - (i + 1) * row_h
            cv.setStrokeColor(C['rule']); cv.setLineWidth(0.4)
            cv.line(key_x, div_y, x + w - 7, div_y)

def draw_card(cv, x, y, w, h, title, accent, rows, key_ratio=0.40):
    card_bg(cv, x, y, w, h, accent, title)
    draw_rows(cv, x, y, w, h - 16, rows, accent, key_ratio)

def draw_modifier_card(cv, x, y, w, h):
    card_bg(cv, x, y, w, h, 'black', 'MODIFIER')
    body_h = h - 16
    COLS, GAP, PAD = 2, 4, 5
    pill_w = (w - 2*PAD - (COLS-1)*GAP) / COLS
    n_rows = len(MODIFIERS) // COLS
    pill_h = (body_h - PAD*2 - (n_rows-1)*GAP) / n_rows
    for i, (key, val, col) in enumerate(MODIFIERS):
        pc = i % COLS; pr = i // COLS
        px = x + PAD + pc*(pill_w+GAP)
        py = y + body_h - PAD - (pr+1)*pill_h - pr*GAP
        cv.setFillColor(C['bg']); cv.setStrokeColor(C['rule']); cv.setLineWidth(0.5)
        cv.roundRect(px, py, pill_w, pill_h, 3, stroke=1, fill=1)
        cv.setFont('Helvetica-Bold', 7); cv.setFillColor(C[col])
        cv.drawString(px+5, py+pill_h-10, key)
        cv.setFont('Helvetica', 6.5); cv.setFillColor(C['muted'])
        cv.drawString(px+5, py+4, val)

def draw_code_box(cv, x, y, w, h, title, accent, code_lines):
    PAD = 7
    card_bg(cv, x, y, w, h, accent, title)
    body_h = h - 16
    term_x, term_y = x+PAD, y+PAD
    term_w, term_h = w-2*PAD, body_h-2*PAD
    cv.setFillColor(colors.HexColor('#1e1e1e'))
    cv.setStrokeColor(colors.HexColor('#333333')); cv.setLineWidth(0.5)
    cv.roundRect(term_x, term_y, term_w, term_h, 4, stroke=1, fill=1)
    dot_y = term_y + term_h - 9
    for di, dc in enumerate(['#ff5f56','#27c93f','#ffbd2e']):
        cv.setFillColor(colors.HexColor(dc))
        cv.circle(term_x+8+di*11, dot_y, 3.5, stroke=0, fill=1)
    fs     = min(7.5, ((term_h-18) / max(len(code_lines),1)) * 0.62)
    line_h = fs * 1.55
    top    = dot_y - 8
    max_w  = term_w - 12
    def draw_line(lx, ly, line):
        s = line.lstrip(); ind = len(line)-len(s)
        iw = cv.stringWidth(' '*ind,'Courier',fs)
        fw = s.split('(')[0].split(' ')[0] if s else ''
        def put(font,col,text,ox=0):
            cv.setFont(font,fs); cv.setFillColor(colors.HexColor(col))
            t=text
            if cv.stringWidth(t,font,fs)>max_w-ox:
                while t and cv.stringWidth(t+'…',font,fs)>max_w-ox: t=t[:-1]
                t+='…'
            cv.drawString(lx+ox,ly,t)
        if not s: return
        if s.startswith('#'): put('Courier','#6a9955',line)
        elif fw in ('def','class'):
            put('Courier-Bold','#569cd6',' '*ind+fw+' ')
            put('Courier','#dcdcaa',line[ind+len(fw)+1:],ox=iw+cv.stringWidth(fw+' ','Courier-Bold',fs))
        elif fw in ('import','from','with','for','if','else','elif','return','while','try','except','sudo','vault'):
            put('Courier-Bold','#c586c0',' '*ind+fw)
            put('Courier','#d4d4d4',line[ind+len(fw):],ox=iw+cv.stringWidth(fw,'Courier-Bold',fs))
        elif '"' in s or "'" in s: put('Courier','#ce9178',line)
        else: put('Courier','#d4d4d4',line)
    for i,line in enumerate(code_lines):
        ly = top - i*line_h
        if ly < term_y+4: break
        draw_line(term_x+6, ly, line)

def draw_formula_card(cv, x, y, w, h):
    card_bg(cv, x, y, w, h, 'black', FORMEL_LABEL)
    body_h = h - 16; fs = 9.5
    total_w = sum(cv.stringWidth(t,'Helvetica-Bold',fs) for t,_ in FORMEL_TEILE)
    fx = x + (w-total_w)/2
    ex_fs = 7
    ex_lines = wrap_text(cv, FORMEL_BEISPIEL,'Helvetica-Oblique',ex_fs,w-20)
    content_h = fs + 6 + len(ex_lines)*9.5+4
    fb = y + body_h - (body_h-content_h)/2 - fs
    cx = fx
    for text,col in FORMEL_TEILE:
        cv.setFont('Helvetica-Bold',fs); cv.setFillColor(C[col])
        cv.drawString(cx,fb,text); cx+=cv.stringWidth(text,'Helvetica-Bold',fs)
    div_y = fb-6
    cv.setStrokeColor(C['rule']); cv.setLineWidth(0.5)
    cv.line(x+10,div_y,x+w-10,div_y)
    cv.setFont('Helvetica-Oblique',ex_fs); cv.setFillColor(C['muted'])
    for li,ln in enumerate(ex_lines): cv.drawString(x+10,div_y-9.5-li*9.5,ln)

def draw_tips_card(cv, x, y, w, h):
    card_bg(cv, x, y, w, h, 'light', TIPS_TITEL)
    draw_rows(cv, x, y, w, h-16, TIPS, 'muted', key_ratio=0.40)

def make_pdf(path):
    cv = canvas.Canvas(path, pagesize=A4)
    cv.setTitle(TITEL)
    M=18; GAP=5; FOOTER_H=18
    cv.setFillColor(C['page_bg']); cv.rect(0,0,W,H,stroke=0,fill=1)
    hdr_y = H-M-20; xc = M
    for pi,word in enumerate(TITEL.split(' ')):
        font = 'Helvetica' if pi==1 else 'Helvetica-Bold'
        col  = C['muted'] if pi==1 else C['header_text']
        cv.setFont(font,17); cv.setFillColor(col)
        cv.drawString(xc,hdr_y,word); xc+=cv.stringWidth(word,font,17)+6
    cv.setFont('Helvetica',6.5); cv.setFillColor(C['footer_text'])
    cv.drawRightString(W-M,hdr_y,UNTERTITEL)
    cv.setStrokeColor(C['header_text']); cv.setLineWidth(1.5)
    rule_y=hdr_y-8; cv.line(M,rule_y,W-M,rule_y)
    content_top=rule_y-GAP; content_h=content_top-(M+FOOTER_H)
    col_w=(W-2*M-2*GAP)/3
    r1_h=content_h*0.435; r3_h=content_h*0.145
    r2_h=content_h-r1_h-r3_h-2*GAP
    y1=content_top-r1_h; y2=y1-GAP-r2_h; y3=y2-GAP-r3_h
    for i,(title,color,rows) in enumerate(SECTIONS[:3]):
        draw_card(cv,M+i*(col_w+GAP),y1,col_w,r1_h,title,color,rows)
    draw_card(cv,M,y2,col_w,r2_h,SECTIONS[3][0],SECTIONS[3][1],SECTIONS[3][2])
    draw_card(cv,M+col_w+GAP,y2,col_w,r2_h,SECTIONS[4][0],SECTIONS[4][1],SECTIONS[4][2])
    draw_modifier_card(cv,M+2*(col_w+GAP),y2,col_w,r2_h)
    fw=col_w*2+GAP
    if CODE_BOX: draw_code_box(cv,M,y3,fw,r3_h,*CODE_BOX)
    else: draw_formula_card(cv,M,y3,fw,r3_h)
    draw_tips_card(cv,M+fw+GAP,y3,col_w,r3_h)
    fy=M+FOOTER_H-4
    cv.setStrokeColor(C['rule']); cv.setLineWidth(0.5); cv.line(M,fy,W-M,fy)
    cv.setFont('Helvetica',6.5); cv.setFillColor(C['footer_text']); cv.drawString(M,fy-8,TITEL)
    cv.setFont('Helvetica-Bold',6.5); cv.setFillColor(C['muted']); cv.drawCentredString(W/2,fy-8,TIPP)
    cv.setFont('Helvetica',6.5); cv.setFillColor(C['footer_text']); cv.drawRightString(W-M,fy-8,'')
    cv.save(); print(f"Done → {path}")

make_pdf('/home/claude/output.pdf')
```
