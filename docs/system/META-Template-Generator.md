# META-TEMPLATE: Template-Generator & Anpassung
> **Trigger:** `[BESCHREIBUNG] - Template-Neu` · `[DATEINAME] - Template-Anpassen`
> **Zweck:** Neues Template erstellen ODER bestehendes anpassen — token-effizient, einmalig, vollständig.

---

## ── MODUS WÄHLEN ──

### MODUS A — Neues Template erstellen
```
Trigger: [BESCHREIBUNG] - Template-Neu

Pflichtfelder (alle in EINER Nachricht):
  TYP:         cheatsheet | research | summary | system | [eigener Typ]
  NAME:        Dateiname ohne Endung (z.B. CS-Druck-Experte-Kompakt)
  ZIEL:        Was soll das Template erzeugen? (1–2 Sätze)
  ZIELGRUPPE:  Wer nutzt es? (Beginner / Experte / beide)
  UMFANG:      Kompakt / Ausführlich / [eigene Definition]
  OUTPUT:      pdf | md | html | [anderes Format]
  CONSTRAINTS: Zeichenlimits, Pflichtfelder, verbotene Änderungen
  TRIGGER:     Wie wird es aufgerufen? (Beispiel-Trigger angeben)
  BEISPIEL:    Optionales Beispiel-Ergebnis oder Referenz-Template
```

### MODUS B — Bestehendes Template anpassen
```
Trigger: [DATEINAME] - Template-Anpassen

Pflichtfelder (alle in EINER Nachricht):
  DATEI:       Pfad oder Raw-URL des bestehenden Templates
  ÄNDERUNG:    Was genau soll geändert werden? (konkret, nicht vage)
  BEHALTEN:    Was darf NICHT verändert werden? (Engine, Layout, etc.)
  GRUND:       Warum die Änderung? (hilft Claude, besser zu entscheiden)
  TEST:        Womit soll das Ergebnis getestet werden?
```

---

## ── CLAUDE-VERHALTEN ──

```
Rolle: Du bist ein Template-Architekt für die PromptTemplateLibary.
       Du optimierst für: Wiederverwendbarkeit · Zeichenlimits · Engine-Stabilität.

Bei Template-Neu:
  1. Prüfe ob ein ähnliches Template bereits existiert → wenn ja, schlage Anpassung vor
  2. Erstelle die vollständige .md-Datei in einem einzigen Output
  3. Füge am Anfang immer einen Kommentarblock mit MODUS / ZIELGRUPPE / UMFANG / OUTPUT ein
  4. Trenne Engine-Code klar von Inhalt durch ── INHALT START ── / ── INHALT END ──
  5. Definiere alle Constraints als Kommentare direkt neben den Feldern
  6. Keine Rückfragen — fehlende Infos mit sinnvollen Defaults füllen und kennzeichnen

Bei Template-Anpassen:
  1. Lade das Template per web_fetch (Raw-URL)
  2. Identifiziere exakt die zu ändernden Zeilen
  3. Gib ONLY den geänderten Block aus (nicht das gesamte Template)
  4. Liste am Ende: was wurde geändert / was wurde bewusst beibehalten
```

---

## ── AUSGABE-FORMAT ──

```
# [TEMPLATE-NAME]
> Trigger: ...
> Typ: ... | Zielgruppe: ... | Umfang: ... | Output: ...

## Constraints
- [Zeichenlimits, Pflichtfelder, verbotene Änderungen]

## Trigger-Beispiel
[THEMA] - [KÜRZEL]

─── INHALT START ───
TITEL        = ""
UNTERTITEL   = ""
[... alle Pflichtfelder des Template-Typs ...]
─── INHALT END ───

[Engine-Code — NIEMALS VERÄNDERN]
```

---

## ── TOKEN-REGELN (für dich als Nutzer) ──

```
✅ IMMER alle Pflichtfelder in EINER Nachricht senden
✅ Bei Anpassungen: nur den diff beschreiben, nicht neu erklären
✅ Existierende Raw-URL mitgeben statt Inhalt copy-pasten
✅ Vage Anweisungen vermeiden → "ändere Farbe von rot zu #1a6b00" statt "mach es grüner"

❌ NICHT in mehreren Nachrichten iterieren ohne klaren Grund
❌ NICHT das gesamte Template in den Chat kopieren wenn URL verfügbar
❌ NICHT nach jedem Schritt bestätigen lassen — erst am Ende testen
```

---

## ── BEKANNTE TEMPLATE-TYPEN & DEFAULTS ──

| Typ | Ordner | Engine | Output | Besonderheit |
|-----|--------|--------|--------|--------------|
| `cheatsheet` | `docs/cheatsheet/` | reportlab | PDF A4 | Engine nie ändern |
| `research` | `docs/research/` | tbd | PDF | in Entwicklung |
| `summary` | `docs/summary/` | tbd | PDF/MD | in Entwicklung |
| `system` | `docs/system/` | — | MD | Projekt-Instruktionen |
| `[neu]` | `docs/[typ]/` | nach Bedarf | nach Bedarf | Typ + Engine definieren |

---

## ── BEISPIEL-AUFRUF ──

### Neu:
```
Cheat Sheet für "Regex Grundlagen", Druck-Beginner-Kompakt - Template-Neu
TYP: cheatsheet
NAME: CS-Druck-Beginner-Kompakt-Regex
ZIEL: Druckfertige Referenzkarte für Regex-Einsteiger
ZIELGRUPPE: Beginner
UMFANG: Kompakt (6–8 Einträge)
OUTPUT: pdf
CONSTRAINTS: Zeichenlimits wie bestehende CS-Templates, Engine unverändert
TRIGGER: Regex Grundlagen - Druck-Beginner-Kompakt
```

### Anpassen:
```
CS-Druck-Experte-Ausfuehrlich - Template-Anpassen
DATEI: https://raw.githubusercontent.com/.../CS-Druck-Experte-Ausfuehrlich.md
ÄNDERUNG: Footer-Text von "Tipp des Tages" zu "Pro-Tipp" umbenennen
BEHALTEN: gesamte Engine, alle Layout-Funktionen, Zeichenlimits
GRUND: Konsistenz mit neuem Branding
TEST: make_pdf ausführen und visuell prüfen
```
