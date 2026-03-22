# Claude Projekt – Template-Bibliothek

## Funktionsweise

Jeder Chat-Start folgt diesem Schema:

```
[THEMA] - [TEMPLATE-NAME]
```

**Beispiele:**
```
Vault Data Standard - Cheatsheet-Druck-Experte-Ausfuehrlich
Git Workflows - Cheatsheet-Web-Beginner-Kompakt
DSGVO Grundlagen - Recherche-Beruflich-Ausfuehrlich
Q3 Ergebnisse - Zusammenfassung-Kompakt
```

---

## Verfügbare Templates

### 📄 Cheat Sheets
| Datei | Trigger | Beschreibung |
|-------|---------|--------------|
| `cheatsheet/CS-Druck-Experte-Ausfuehrlich.md` | Druck + Experte + Ausführlich | Volle Tiefe, Druckausgabe |
| `cheatsheet/CS-Druck-Experte-Kompakt.md` | Druck + Experte + Kompakt | Kerninfos, Druckausgabe |
| `cheatsheet/CS-Druck-Beginner-Ausfuehrlich.md` | Druck + Beginner + Ausführlich | Erklärt, Druckausgabe |
| `cheatsheet/CS-Druck-Beginner-Kompakt.md` | Druck + Beginner + Kompakt | Einfach & kurz, Druck |
| `cheatsheet/CS-Web-Experte-Ausfuehrlich.md` | Web + Experte + Ausführlich | Volle Tiefe, Bildschirm |
| `cheatsheet/CS-Web-Experte-Kompakt.md` | Web + Experte + Kompakt | Kerninfos, Bildschirm |
| `cheatsheet/CS-Web-Beginner-Ausfuehrlich.md` | Web + Beginner + Ausführlich | Erklärt, Bildschirm |
| `cheatsheet/CS-Web-Beginner-Kompakt.md` | Web + Beginner + Kompakt | Einfach & kurz, Web |

### 🔍 Recherche *(in Vorbereitung)*
| Datei | Trigger |
|-------|---------|
| `research/Recherche-Beruflich-Ausfuehrlich.md` | Beruflich + Ausführlich |
| `research/Recherche-Beruflich-Kompakt.md` | Beruflich + Kompakt |
| `research/Recherche-Privat-Ausfuehrlich.md` | Privat + Ausführlich |

### 📋 Zusammenfassungen *(in Vorbereitung)*
| Datei | Trigger |
|-------|---------|
| `summary/Summary-Ausfuehrlich.md` | Ausführlich |
| `summary/Summary-Kompakt.md` | Kompakt |

### 📊 Präsentationen *(in Vorbereitung)*
| Datei | Trigger |
|-------|---------|
| `presentation/Praesentation-Beruflich.md` | Beruflich |

---

## Projekt-Instruktion (als Projekt-Prompt hinterlegen)

```
Du hast Zugriff auf eine Template-Bibliothek in den Projektdateien.

Wenn ich einen Chat mit "[THEMA] - [TEMPLATE-NAME]" starte:
1. Lade das passende Template aus den Projektdateien
2. Fülle es mit dem genannten Thema aus
3. Erstelle die PDF ohne Rückfragen

Cheat Sheet Varianten:
- "Druck" → weißer Hintergrund, druckoptimiert
- "Web"   → dunkler Hintergrund, bildschirmoptimiert
- "Experte" → Fachbegriffe, keine Grundlagen-Erklärungen
- "Beginner" → einfache Sprache, Erklärungen bei Fachbegriffen
- "Ausführlich" → 10–12 Einträge pro Karte, Code-Box JA
- "Kompakt" → 6–8 Einträge pro Karte, Code-Box NEIN
```

---

## Tipps

- **Thema präzise formulieren** → bessere Inhalte
- **Kombination frei wählbar** → auch "Druck-Beginner-Ausführlich" funktioniert
- **Pro Thema ein neuer Chat** → verhindert Kontext-Vermischung
