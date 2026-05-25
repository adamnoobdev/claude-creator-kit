---
name: elevenlabs
description: Generera musik eller ljudeffekter via ElevenLabs API. Trigger när användaren säger "generera musik", "skapa låt", "ljudeffekt", "sfx", "background music", eller behöver audio till ett projekt.
---

## Vad det är

ElevenLabs har två generativa audio-modeller:
- **Music**: skapar bakgrundsmusik från text-prompt (genre, instrument, tempo)
- **Sound Effects**: korta ljudeffekter (whoosh, impact, ambience, etc.)

Båda anropas via samma `ELEVENLABS_API_KEY`.

## Var det bor

- Skript: `tools/generate_elevenlabs.py` (skapa själv när du behöver det)
- Default output: `projects/<projekt>/assets/audio/`
- API-key: `ELEVENLABS_API_KEY` i `.env`

## Anrop: Music

```bash
curl -X POST https://api.elevenlabs.io/v1/music \
  -H "xi-api-key: $ELEVENLABS_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "<din musik-prompt>",
    "music_length_ms": 30000
  }' \
  --output projects/<projekt>/assets/audio/musik.mp3
```

## Anrop: Sound Effects

```bash
curl -X POST https://api.elevenlabs.io/v1/sound-generation \
  -H "xi-api-key: $ELEVENLABS_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "<sfx-beskrivning>",
    "duration_seconds": 3
  }' \
  --output projects/<projekt>/assets/audio/sfx.mp3
```

## Prompt-tips

### Musik
- Beskriv genre och era, INTE artistnamn. "in the style of X" ger HTTP 400 (ToS-violation).
- Exempel: "uplifting indie folk with acoustic guitar, light percussion, 120 BPM, 60s era warmth"
- Specificera mood: "uplifting", "melancholic", "intense", "calm"
- Inkludera instrument: "piano-driven", "with strings", "drum-and-bass"

### SFX
- Var konkret: "metallic clang on concrete, short reverb"
- Specificera material: "wood creak", "glass break", "fabric rustle"
- Inkludera akustik: "in a small room", "outdoors", "in a cave"

## Begränsningar

- Musik: max 5 min per generation, ~30-90 sek genererings-tid
- SFX: max 22 sek
- Free-tier har månads-credits-cap

## Docs

[elevenlabs.io/docs/api-reference](https://elevenlabs.io/docs/api-reference)
