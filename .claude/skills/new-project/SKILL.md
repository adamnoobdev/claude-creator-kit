---
name: new-project
description: Skapar en ny projektmapp under `projects/` med standardstruktur (briefs, assets, animations, exports). Trigger när användaren säger "skapa nytt projekt", "starta projekt", "/new-project", eller börjar på något nytt.
---

## Vad det gör

Kopierar `templates/project/` till `projects/<projektnamn>/` så du har en ren mapp med rätt struktur.

## Hur du kör

```bash
# Från claude-creator-kit-roten
cp -r templates/project projects/<projektnamn>
```

Eller be Claude direkt:

> Skapa ett nytt projekt som heter "<projektnamn>"

Claude ska:
1. Kontrollera att `projects/<projektnamn>/` inte redan finns
2. Kopiera `templates/project/` dit
3. Bekräfta att mappen är skapad och visa strukturen
4. Fråga vad projektet handlar om så `README.md` kan fyllas i

## Standard-mappstruktur

```
projects/<projektnamn>/
├── README.md           ← projekt-context (fyll i)
├── briefs/             ← beställningar, manus, idéer
├── assets/
│   ├── stills/         ← genererade och hämtade bilder
│   ├── audio/          ← musik, sfx, voiceover
│   └── video/          ← clips att klippa från
├── animations/         ← hyperframes-projekt (om relevant)
└── exports/            ← klara filer för leverans
```

## Namnkonvention

- Kebab-case: `min-video-2026`, `kund-x-reel`
- Inga mellanslag eller specialtecken
- Datum-prefix om kronologi är viktigt: `2026-05-portratt-jens`
