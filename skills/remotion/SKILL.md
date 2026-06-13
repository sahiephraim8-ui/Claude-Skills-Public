---
name: remotion
description: Créer des compositions vidéo animées avec Remotion (React + TypeScript). Déclencher quand l'utilisateur demande une vidéo, un montage, une animation exportable en MP4/GIF, une intro, une annonce, un reel, une présentation vidéo, ou tout rendu motion design. Gère setup projet, création de compositions, render CLI, et patterns avancés.
---

# Remotion — Skill Vidéo & Motion Design

Remotion permet de créer des vidéos avec React + TypeScript. Chaque frame est un render React. On export en MP4, GIF, WebM.

---

## Setup rapide (nouveau projet)

```bash
npm install remotion @remotion/cli @remotion/player
```

Structure minimale :
```
src/remotion/
├── index.ts          ← entry point
├── Root.tsx          ← enregistre les compositions
└── compositions/
    └── MaVideo.tsx   ← la composition
```

**`src/remotion/index.ts`**
```ts
import { registerRoot } from 'remotion'
import { RemotionRoot } from './Root'
registerRoot(RemotionRoot)
```

**`remotion.config.ts`** (racine du projet)
```ts
import { Config } from '@remotion/cli/config'
Config.setVideoImageFormat('jpeg')
Config.setOverwriteOutput(true)
Config.setEntryPoint('./src/remotion/index.ts')
```

---

## APIs essentielles

```tsx
import {
  AbsoluteFill,      // div 100% width/height, position absolute
  useCurrentFrame,   // frame actuelle (0, 1, 2, ...)
  useVideoConfig,    // { fps, width, height, durationInFrames }
  interpolate,       // mappage de valeurs entre ranges
  spring,            // animation physique spring
  Sequence,          // décale le début d'un bloc de frames
  Audio,             // audio dans la vidéo
  Img,               // image dans la vidéo
  Video,             // vidéo dans la vidéo
  staticFile,        // référence un fichier dans /public
} from 'remotion'
```

### `interpolate` — la fonction clé
```ts
// interpolate(valeur, [inputRange], [outputRange], options)
const opacity = interpolate(frame, [0, 30], [0, 1], {
  extrapolateLeft: 'clamp',
  extrapolateRight: 'clamp',
})
// frame 0 → opacity 0, frame 30 → opacity 1, clampé après
```

### `spring` — animations naturelles
```ts
const scale = spring({
  frame,
  fps,
  config: {
    damping: 16,    // amortissement (plus haut = moins de rebond)
    stiffness: 120, // rigidité (plus haut = plus rapide)
    mass: 1,
  },
  delay: 10,        // commence à la frame 10
})
```

### `Sequence` — décalage temporel
```tsx
<Sequence from={30} durationInFrames={60}>
  {/* Visible seulement entre frame 30 et 90 */}
  <MonComposant />
</Sequence>
```

---

## Enregistrer une composition

```tsx
// Root.tsx
import { Composition } from 'remotion'
import { MaVideo } from './compositions/MaVideo'

export function RemotionRoot() {
  return (
    <Composition
      id="MaVideo"                // nom utilisé dans le CLI render
      component={MaVideo}
      durationInFrames={150}      // 150 frames ÷ 30fps = 5 secondes
      fps={30}
      width={1080}
      height={1080}               // 1:1 Instagram. 1920×1080 = 16:9. 1080×1920 = 9:16 Stories
      defaultProps={{             // props avec valeurs par défaut
        titre: 'Mon Titre',
        couleur: '#7C3AED',
      }}
    />
  )
}
```

---

## Formats vidéo standards

| Usage | Width | Height | Ratio |
|-------|-------|--------|-------|
| Instagram Post | 1080 | 1080 | 1:1 |
| Instagram/TikTok Stories | 1080 | 1920 | 9:16 |
| YouTube / Présentation | 1920 | 1080 | 16:9 |
| LinkedIn Banner | 1584 | 396 | 4:1 |
| Twitter/X | 1280 | 720 | 16:9 |

---

## Patterns de composition — Template de base

```tsx
import { AbsoluteFill, interpolate, spring, useCurrentFrame, useVideoConfig } from 'remotion'

interface Props {
  titre: string
  sousTitre?: string
  couleurPrimaire?: string
}

export function MaComposition({ titre, sousTitre = '', couleurPrimaire = '#7C3AED' }: Props) {
  const frame = useCurrentFrame()
  const { fps } = useVideoConfig()

  // --- Animations ---
  const titreOpacity = interpolate(frame, [0, 25], [0, 1], { extrapolateRight: 'clamp' })
  const titreY = interpolate(frame, [0, 25], [30, 0], { extrapolateRight: 'clamp' })
  const sousTitreOpacity = interpolate(frame, [20, 45], [0, 1], { extrapolateRight: 'clamp' })
  const exitOpacity = interpolate(frame, [120, 150], [1, 0], { extrapolateLeft: 'clamp' })

  const logoScale = spring({ frame, fps, config: { damping: 16, stiffness: 120 } })

  return (
    <AbsoluteFill style={{
      background: 'linear-gradient(145deg, #050A18 0%, #091228 100%)',
      fontFamily: 'Inter, system-ui, sans-serif',
      opacity: exitOpacity,
    }}>
      {/* Fond grille */}
      <AbsoluteFill style={{
        backgroundImage: `
          linear-gradient(rgba(99,130,255,0.04) 1px, transparent 1px),
          linear-gradient(90deg, rgba(99,130,255,0.04) 1px, transparent 1px)
        `,
        backgroundSize: '60px 60px',
      }} />

      {/* Glow central */}
      <AbsoluteFill style={{
        background: `radial-gradient(ellipse 500px 400px at 50% 50%, ${couleurPrimaire}28 0%, transparent 70%)`,
      }} />

      {/* Contenu */}
      <AbsoluteFill style={{
        display: 'flex', flexDirection: 'column',
        alignItems: 'center', justifyContent: 'center', gap: 20,
        padding: '0 80px',
      }}>
        <div style={{
          fontSize: 72, fontWeight: 800, color: '#FFFFFF',
          letterSpacing: '-0.05em', textAlign: 'center',
          opacity: titreOpacity,
          transform: `translateY(${titreY}px)`,
        }}>
          {titre}
        </div>

        {sousTitre && (
          <div style={{
            fontSize: 28, fontWeight: 400,
            color: 'rgba(255,255,255,0.55)',
            textAlign: 'center',
            opacity: sousTitreOpacity,
          }}>
            {sousTitre}
          </div>
        )}
      </AbsoluteFill>
    </AbsoluteFill>
  )
}
```

---

## Patterns avancés

### Texte mot par mot (typewriter)
```tsx
function WordReveal({ text, startFrame }: { text: string; startFrame: number }) {
  const frame = useCurrentFrame()
  const words = text.split(' ')
  return (
    <span>
      {words.map((word, i) => {
        const opacity = interpolate(
          frame - startFrame,
          [i * 4, i * 4 + 8],
          [0, 1],
          { extrapolateLeft: 'clamp', extrapolateRight: 'clamp' }
        )
        return (
          <span key={i} style={{ opacity, marginRight: 12 }}>{word}</span>
        )
      })}
    </span>
  )
}
```

### Compteur animé (stats)
```tsx
function Counter({ from, to, startFrame }: { from: number; to: number; startFrame: number }) {
  const frame = useCurrentFrame()
  const value = Math.round(
    interpolate(frame - startFrame, [0, 60], [from, to], {
      extrapolateLeft: 'clamp',
      extrapolateRight: 'clamp',
    })
  )
  return <span>{value.toLocaleString('fr-FR')}</span>
}
```

### Barre de progression
```tsx
function ProgressBar({ progress, frame, startFrame }: { progress: number; frame: number; startFrame: number }) {
  const width = interpolate(frame - startFrame, [0, 45], [0, progress], {
    extrapolateLeft: 'clamp', extrapolateRight: 'clamp',
  })
  return (
    <div style={{ width: '100%', height: 4, background: 'rgba(255,255,255,0.1)', borderRadius: 999 }}>
      <div style={{ width: `${width}%`, height: '100%', background: '#2ECC71', borderRadius: 999 }} />
    </div>
  )
}
```

### Particules flottantes
```tsx
function Particles({ frame }: { frame: number }) {
  const dots = [
    { x: 15, y: 20, delay: 0, color: 'rgba(99,130,255,0.6)' },
    { x: 80, y: 15, delay: 5, color: 'rgba(200,169,110,0.5)' },
    { x: 90, y: 70, delay: 10, color: 'rgba(99,130,255,0.4)' },
  ]
  return (
    <AbsoluteFill style={{ pointerEvents: 'none' }}>
      {dots.map((d, i) => {
        const f = Math.max(0, frame - d.delay)
        const opacity = interpolate(f, [0, 15], [0, 1], { extrapolateRight: 'clamp' })
        const y = interpolate(f, [0, 130], [0, -40], { extrapolateRight: 'clamp' })
        return (
          <div key={i} style={{
            position: 'absolute',
            left: `${d.x}%`, top: `${d.y}%`,
            width: 4, height: 4, borderRadius: '50%',
            background: d.color, opacity,
            transform: `translateY(${y}px)`,
            boxShadow: `0 0 8px ${d.color}`,
          }} />
        )
      })}
    </AbsoluteFill>
  )
}
```

### Badge animé (pill)
```tsx
function Badge({ label, color, frame }: { label: string; color: string; frame: number }) {
  const scale = spring({ frame, fps: 30, config: { damping: 14, stiffness: 140 } })
  const opacity = interpolate(frame, [0, 8], [0, 1], { extrapolateRight: 'clamp' })
  return (
    <div style={{
      transform: `scale(${scale})`, opacity,
      background: `${color}20`,
      border: `1px solid ${color}55`,
      borderRadius: 999, padding: '8px 20px',
      fontSize: 14, fontWeight: 700, color,
      letterSpacing: '0.1em', textTransform: 'uppercase',
    }}>
      {label}
    </div>
  )
}
```

---

## Commandes CLI

```bash
# Studio interactif (hot-reload, preview en temps réel)
npx remotion studio

# Render MP4
npx remotion render <CompositionId> output/video.mp4

# Render avec props custom
npx remotion render MaVideo output/video.mp4 --props='{"titre":"Hello","couleur":"#2ECC71"}'

# Render GIF
npx remotion render MaVideo output/video.gif --codec=gif

# Render frame précise (debug)
npx remotion still MaVideo output/frame.png --frame=45

# Render avec qualité
npx remotion render MaVideo output/video.mp4 --crf=18 --codec=h264
```

---

## Workflow demande vidéo

Quand l'utilisateur demande une vidéo, collecter ces infos :
1. **Contenu** — textes, données, logos, couleurs de la marque
2. **Format** — 1:1 / 9:16 / 16:9 et durée souhaitée
3. **Style** — dark/light, minimaliste/bold, couleur dominante
4. **Usage** — Instagram, YouTube, présentation, GIF Slack

Puis :
1. Créer la composition dans `src/remotion/compositions/NomVideo.tsx`
2. L'enregistrer dans `src/remotion/Root.tsx`
3. Donner la commande de render exacte à exécuter

---

## Règles de qualité

- Toujours `extrapolateLeft: 'clamp'` et `extrapolateRight: 'clamp'` sur les `interpolate` pour éviter les valeurs hors bornes
- Exit fade systématique : `interpolate(frame, [durationInFrames - 20, durationInFrames], [1, 0], { extrapolateLeft: 'clamp' })`
- Polices : utiliser `Inter`, `system-ui` — pas de fonts externes sans vérification disponibilité
- Pas de `position: fixed` — utiliser `AbsoluteFill` ou `position: absolute`
- Pour les couleurs avec transparence : préférer `rgba(r,g,b,a)` plutôt que hex+alpha pour la lisibilité
- Props toujours typées avec interface TypeScript explicite
- Jamais de `any`
