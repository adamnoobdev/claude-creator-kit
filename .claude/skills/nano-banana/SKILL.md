---
name: nano-banana
description: Generera bilder via Kie.ai (Googles Nano Banana 2-modell). Trigger när användaren säger "generera bild", "skapa still", "nano banana", "bildgenerering", eller behöver visuella assets till ett projekt.
---

## Vad det är

Nano Banana 2 är Google Geminis bildgenerator. Kie.ai är en wrapper som ger åtkomst via ett enkelt API. Bra för:
- Stills till video-projekt
- Character-portraits
- Product-shots
- Background plates

## Var det bor

- Skriptet: `tools/generate_nano_banana.py` (skapa själv när du behöver det)
- Default output: `projects/<projekt>/assets/stills/`
- API-key: `KIE_API_KEY` i `.env`

## Anrop direkt mot Kie.ai

```bash
curl -X POST https://api.kie.ai/v1/images/generations \
  -H "Authorization: Bearer $KIE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "google/nano-banana-2",
    "prompt": "<din prompt>",
    "aspect_ratio": "9:16",
    "n": 1
  }'
```

Responsen innehåller en URL till bilden, ladda ner med `curl -o`.

## Prompt-tips

- Var specifik om stil: "photorealistic", "fine cinematic grain", "35mm lens"
- Specificera komposition: "close-up", "wide shot", "medium shot"
- Undvik fake branding: skriv "no text, no logos" om du inte vill ha varumärken
- Beskriv ljus: "soft natural light", "harsh sunlight", "blue hour"
- Negativa instruktioner funkar: "no people in background", "no watermark"

## Begränsningar

- ~10-30 sek per bild
- Vissa prompts triggar safety-filter (våld, NSFW, kända personer)
- Inga garanterade exakta resultat. Iterera vid behov.

## Pricing

Se [kie.ai/pricing](https://kie.ai/pricing). Free-tier räcker för test.
