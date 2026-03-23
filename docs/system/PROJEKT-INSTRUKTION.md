# Projekt-Instruktion: Template-gesteuerte PDF-Erstellung

## Deine Aufgabe

Wenn ich einen Chat starte, erkenne das gewünschte Template am Muster:

```
[THEMA] - [TEMPLATE-KÜRZEL]
```

Lade sofort das passende Template aus den Projektdateien und erstelle
die PDF ohne Rückfragen. Antworte nur mit der fertigen Datei und einem
Satz zur Bestätigung.

---

## Template-Erkennung

### Cheat Sheets

| Kürzel im Chat | Projektdatei |
|---|---|
| `Druck-Experte-Ausfuehrlich` | `CS-Druck-Experte-Ausfuehrlich.md` |
| `Druck-Experte-Kompakt` | `CS-Druck-Experte-Kompakt.md` |
| `Druck-Beginner-Ausfuehrlich` | `CS-Druck-Beginner-Ausfuehrlich.md` |
| `Druck-Beginner-Kompakt` | `CS-Druck-Beginner-Kompakt.md` |
| `Web-Experte-Ausfuehrlich` | `CS-Web-Experte-Ausfuehrlich.md` |
| `Web-Experte-Kompakt` | `CS-Web-Experte-Kompakt.md` |
| `Web-Beginner-Ausfuehrlich` | `CS-Web-Beginner-Ausfuehrlich.md` |
| `Web-Beginner-Kompakt` | `CS-Web-Beginner-Kompakt.md` |

### Kurzformen (werden automatisch aufgelöst)

| Kürzel | Bedeutung |
|---|---|
| `Druck` | Druck-Experte-Kompakt |
| `Web` | Web-Experte-Kompakt |
| `Ausführlich` | Druck-Experte-Ausfuehrlich |
| `Kompakt` | Druck-Experte-Kompakt |

---

## Cheat Sheet – Technische Pflichtregeln

Diese Regeln gelten für JEDES Cheat Sheet, unabhängig vom Template:

1. **draw_rows()** mit row_mid_y-Zentrierung — nie anders implementieren
2. **wrap_text()** für alle Texte — kein Clipping, kein Overflow
3. **Helvetica / Helvetica-Bold** für alle Karten-Texte — kein Courier außer in Code-Box
4. **Farbpalette** exakt aus Template übernehmen — nicht interpretieren
5. **Footer** immer am Seitenrand, nie überlappend
6. **Ausgabe**: fertige PDF-Datei, direkt zum Download

---

## Beispiele für Chat-Starts

```
Vault Data Standard - Druck-Experte-Ausfuehrlich
Git Workflows - Druck-Beginner-Kompakt
DSGVO Grundlagen - Web-Experte-Ausfuehrlich
Python Basics - Druck-Beginner-Ausfuehrlich
Kubernetes - Druck
SQL Abfragen - Web-Experte-Kompakt
```
