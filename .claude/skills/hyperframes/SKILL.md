---
name: hyperframes
description: Bygg 9:16-animationer från HTML+GSAP och rendera till MP4. Trigger när användaren säger "hyperframes", "html till video", "gsap-animation", "9:16 animation", "rendra animation", eller jobbar i en `animations/`-mapp.
---

## Vad HyperFrames är

En open-source HTML-till-video-pipeline från HeyGen ([github.com/heygen-com/hyperframes](https://github.com/heygen-com/hyperframes)). Tar en `index.html` med GSAP-timeline, renderar via Puppeteer + FFmpeg till MP4.

Bra för: snabba branded animations (text-cards, bars, charts, CTA-overlays) som klipps in i Premiere ovanpå live-action.

## Mappstruktur (per projekt)

```
projects/<projekt>/animations/
  index.html          ← active animation
  assets/
    fonts/            ← .woff2-filer
    *.png             ← logos, brand-assets
  hyperframes.json
  package.json
  renders/            ← render-outputs
```

## Setup ett nytt animations-projekt

```bash
cd projects/<projekt>/animations
npx -y hyperframes init .
```

Verifiera att Node 22+ och FFmpeg finns:

```bash
node --version    # >= 22
ffmpeg -version
```

## Workflow

### 1. Skriv eller kopiera HTML

```html
<div id="root" data-composition-id="main"
     data-start="0" data-duration="7"
     data-width="1080" data-height="1920">
  <div id="stage" class="stage clip"
       data-start="0" data-duration="7" data-track-index="1">
    <!-- content här -->
  </div>
</div>
```

`data-composition-id`, `data-duration`, `data-track-index` är required.

### 2. GSAP timeline-mönster

```html
<script>
  window.__timelines = window.__timelines || {};
  const tl = gsap.timeline({ paused: true });

  tl.from("#element", { opacity: 0, duration: 0.7, ease: "power2.out" }, 0.1);
  tl.to({}, { duration: 1.0 }, 1.7);
  tl.to("#element", { y: -200, duration: 0.5, ease: "power2.inOut" }, 2.5);

  window.__timelines["main"] = tl;
</script>
```

`window.__timelines["<composition-id>"] = tl` är hur HyperFrames driver timelinen.

### 3. Validera

```bash
npx --yes hyperframes lint
```

### 4. Render

```bash
# Draft (snabb iteration)
npx --yes hyperframes render -o renders/test-draft.mp4 -q draft -f 30

# Final (delivery)
npx --yes hyperframes render -o renders/final.mp4 -q high -f 30
```

Quality: `draft` / `standard` / `high`. fps: 30 default för paid social.

### 5. Verifiera visuellt

```bash
ffmpeg -y -i renders/final.mp4 \
  -vf "select=eq(n\,60)+eq(n\,150)" \
  -vsync vfr /tmp/frame_%02d.png
```

Frame N = sekund × fps. 30fps: frame 60 = 2s, frame 150 = 5s.

## Regler

1. Använd `power2.out` / `power3.out` / `power2.inOut` eases. Aldrig `back.out`, `elastic.out`, `bounce.out` om inte användaren explicit vill ha leksak-känsla.
2. 9:16 default: 1080×1920. Bara 16:9 om användaren ber.
3. 30fps default. 60fps bara om animation kräver smooth motion.
4. `will-change: top, height, opacity` på animerade element.
5. Total `top + height` ska vara inom canvas-höjd, annars klipps element av.

## Vanliga fel

| Symptom | Fix |
|---|---|
| `command not found: hyperframes` | Använd `npx --yes hyperframes ...` (auto-installerar) |
| "module not found" på fonts | Fonts ska ligga i `assets/fonts/` |
| Element osynliga | `top + height` utanför canvas, kolla CSS |
| Render hänger | Använd `-q draft` för iteration |
| Text wrap:ar oväntat | `white-space: nowrap` på text-element |

## Se även

- HyperFrames GitHub: [github.com/heygen-com/hyperframes](https://github.com/heygen-com/hyperframes)
- GSAP docs: [greensock.com/docs/v3/GSAP](https://greensock.com/docs/v3/GSAP)
