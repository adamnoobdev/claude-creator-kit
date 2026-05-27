---
name: elevenlabs
description: Generera musik, ljudeffekter eller dubba video/audio till andra språk via ElevenLabs API. Trigger när användaren säger "generera musik", "skapa låt", "ljudeffekt", "sfx", "background music", "dubba", "översätt video", "voiceover på engelska", eller behöver audio till ett projekt.
---

## Vad det är

ElevenLabs har tre generativa audio-funktioner:
- **Music**: skapar bakgrundsmusik från text-prompt (genre, instrument, tempo)
- **Sound Effects**: korta ljudeffekter (whoosh, impact, ambience, etc.)
- **Dubbing**: översätter och dubbar video/audio till andra språk, behåller talarens röstkaraktär

Alla anropas via samma `ELEVENLABS_API_KEY`.

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

## Anrop: Dubbing

Dubbning körs i tre steg: starta jobb, polla status, ladda ner.

### 1. Starta dubbnings-jobb

```bash
curl -X POST https://api.elevenlabs.io/v1/dubbing \
  -H "xi-api-key: $ELEVENLABS_API_KEY" \
  -F "file=@projects/<projekt>/assets/video/original.mp4" \
  -F "target_lang=en" \
  -F "source_lang=sv" \
  -F "num_speakers=0"
```

Svaret innehåller ett `dubbing_id`. `target_lang`/`source_lang` är ISO 639-1-koder (sv, en, de, es, fr...). `num_speakers=0` auto-detekterar antalet talare.

Användbara flaggor:
- `drop_background_audio=true` tar bort originalljud bakom rösten
- `disable_voice_cloning=true` använder standard-röster istället för att klona talaren
- `highest_resolution=true` för video-output i full kvalitet
- `target_accent` (experimentell) styr accent i målspråket

### 2. Kolla status

```bash
curl https://api.elevenlabs.io/v1/dubbing/<dubbing_id> \
  -H "xi-api-key: $ELEVENLABS_API_KEY"
```

Fältet `status` blir `dubbed` när det är klart. Polla med ~10 sek mellanrum.

### 3. Ladda ner resultatet

```bash
curl https://api.elevenlabs.io/v1/dubbing/<dubbing_id>/audio/en \
  -H "xi-api-key: $ELEVENLABS_API_KEY" \
  --output projects/<projekt>/exports/dubbed-en.mp4
```

Språkkoden i URL:en matchar `target_lang`.

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
- Dubbning: audio-dubbning, läppsynk matchar inte alltid perfekt (syns i talking-head närbild). Maskinöversättningen bör korrekturläsas innan sändning. Review alltid output för broadcast-kvalitet.
- Free-tier har månads-credits-cap. Dubbning drar mer credits än musik/sfx.

## Docs

[elevenlabs.io/docs/api-reference](https://elevenlabs.io/docs/api-reference)
