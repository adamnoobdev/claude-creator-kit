# Claude Creator Kit

En öppen startpunkt för creators som vill använda Claude till att producera video, bild och ljud snabbare.

Klona repot, fyll i tre API-nycklar, och du har verktyg för att klippa video, generera bilder, skapa animationer och göra musik. Allt via samtal med Claude i din kodeditor. Ingen kod du behöver lära dig.

## Vad du får

- **video-use**: klipp video, transkribera tal, lägg på subtitles
- **hyperframes**: 9:16-animationer från HTML+GSAP till MP4 (Reels, TikTok)
- **nano-banana**: generera bilder via Kie.ai (Googles Nano Banana 2)
- **elevenlabs**: musik och ljudeffekter via ElevenLabs API
- **new-project**: scaffoldar en mapp för ett nytt projekt med rätt struktur

## Kom igång

### 1. Installera VS Code

Ladda ner från [code.visualstudio.com](https://code.visualstudio.com). Det är miljön du jobbar i.

### 2. Installera Claude-extension i VS Code

I VS Code: öppna Extensions (Cmd+Shift+X på Mac, Ctrl+Shift+X på Windows), sök "Claude Code", klicka Install. Logga in när du blir promptad.

### 3. Installera Node, FFmpeg och Python

Behövs för rendering och API-anrop. På Mac:

```bash
brew install node ffmpeg python
```

Saknar du Homebrew? Installera från [brew.sh](https://brew.sh) först.

På Windows: ladda ner från [nodejs.org](https://nodejs.org), [ffmpeg.org](https://ffmpeg.org/download.html), [python.org](https://python.org).

### 4. Ladda ner kit:et

```bash
git clone https://github.com/adamnoobdev/claude-creator-kit.git
```

Eller [ladda ner som ZIP](https://github.com/adamnoobdev/claude-creator-kit/archive/refs/heads/main.zip).

### 5. Fyll i dina API-nycklar

Öppna mappen i VS Code. Kopiera `.env.example` till `.env` och klistra in nycklar från:

- [console.anthropic.com](https://console.anthropic.com) (Claude API)
- [kie.ai](https://kie.ai) (Nano Banana 2)
- [elevenlabs.io](https://elevenlabs.io) (musik och sfx)

Alla har gratis-tier som räcker för att testa.

### 6. Säg till Claude: "Hjälp mig komma igång"

Öppna Claude-panelen i VS Code och skriv det. Claude tar det därifrån.

## Mappstruktur

```
claude-creator-kit/
├── .claude/skills/      ← verktygen Claude kan använda
├── templates/project/   ← mallen för nya projekt
├── projects/            ← här hamnar dina projekt
└── web/                 ← landningssida
```

## Licens

MIT. Fork:a, modifiera, använd kommersiellt.
