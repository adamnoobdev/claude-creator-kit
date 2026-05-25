# Claude Creator Kit

En startpunkt för dig som vill använda Claude Code till att producera video och bild snabbare.

Klona repot, fyll i tre API-nycklar, och du har verktyg för att klippa video, generera bilder, skapa animationer och göra musik. Inget hemligt eller magiskt. Bara en organiserad mapp och några små skripts som anropar AI-tjänster åt dig.

## Vad du får

- **video-use**: klipp video, transkribera tal, lägg på subtitles. Klart via samtal med Claude.
- **hyperframes**: bygg 9:16-animationer i HTML och rendera till MP4. Bra för Reels och TikTok-overlays.
- **nano-banana**: generera bilder via Kie.ai (Googles Nano Banana 2-modell).
- **elevenlabs**: skapa musik och ljudeffekter via ElevenLabs API.
- **new-project**: skapar en mapp för ett nytt projekt med rätt struktur.

## Vad du behöver

1. **Claude Code installerat**. Se [claude.com/code](https://claude.com/code).
2. **Node.js 22+** och **FFmpeg**. På Mac: `brew install node ffmpeg`.
3. **Python 3.10+** för skripten.
4. **Tre API-nycklar** (gratis-tier räcker för att testa):
   - Anthropic (för Claude API-anrop, om du vill köra automations utöver Claude Code): [console.anthropic.com](https://console.anthropic.com)
   - Kie.ai (för Nano Banana 2): [kie.ai](https://kie.ai)
   - ElevenLabs (för musik och sfx): [elevenlabs.io](https://elevenlabs.io)

## Kom igång

```bash
# 1. Klona repot
git clone https://github.com/adamnoobdev/claude-creator-kit.git
cd claude-creator-kit

# 2. Kopiera .env.example till .env och fyll i nycklarna
cp .env.example .env

# 3. Starta Claude Code i mappen
claude
```

I Claude Code, säg t.ex. `/new-project min-forsta-video` så scaffoldar Claude en projektmapp åt dig.

## Mappstruktur

```
claude-creator-kit/
├── .claude/skills/      ← verktygen Claude kan använda
├── templates/project/   ← mallen för nya projekt
├── projects/            ← här hamnar dina projekt
└── web/                 ← landningssida (kan ignoreras)
```

## Hjälp

Be Claude direkt: `Hjälp mig komma igång` eller `Vad kan du göra här?`

## Licens

MIT. Fork:a, modifiera, använd kommersiellt.
