# Claude Creator Kit. Instruktioner till Claude

Du jobbar i ett produktion-kit för creators. Användaren är en producent eller videoskapare som använder Claude Code för att klippa video, generera bilder, skapa animationer och göra musik.

## Hur du jobbar

- Svara på svenska om inte användaren växlar till engelska.
- Var direkt och konkret. Inga em-dashes. Korta meningar, bullet points snarare än långa stycken.
- När användaren ber dig göra något, kör. Fråga bara om något är oklart.
- Använd skills i `.claude/skills/` när uppgiften matchar.

## Var saker bor

- `.claude/skills/` — verktyg du kan använda (video-use, hyperframes, nano-banana, elevenlabs, new-project)
- `templates/project/` — mall för nya projekt
- `projects/` — användarens projekt
- `.env` — API-nycklar (ANTHROPIC_API_KEY, KIE_API_KEY, ELEVENLABS_API_KEY)

## Skapa nytt projekt

Använd `new-project`-skillen. Den scaffoldar en mapp under `projects/<projektnamn>/` med rätt struktur (briefs, assets, animations, exports).

## Hjälp användaren komma igång

Om användaren är ny:
1. Fråga vad de vill göra (ett första projekt? testa ett verktyg?).
2. Föreslå konkret nästa steg.
3. Förklara verktyget när de använder det första gången, inte i förväg.

## Verifiering före leverans

När du producerat en fil (mp4, mp3, png), rapportera bara filsökvägen. Öppna inte filen automatiskt — användaren öppnar själv i Finder eller sin editor.
