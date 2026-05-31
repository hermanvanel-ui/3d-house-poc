# 3D House — POC scroll cinématique

Proof of concept : **une seule page**, tu scrolles, et la caméra voyage dans la maison 3D. Chaque chapitre = une pièce du siège virtuel a.SYNC. Pattern type **Apple AirPods Pro / NYT scrollytelling / Lusion**.

## 🎮 Comment tester

- **GitHub Pages (live)** : <https://hermanvanel-ui.github.io/3d-house-poc/>
- **Local** : double-clique sur `index.html` (Three.js + Lenis chargés via CDN, aucun build).
- **Netlify drop** : glisse le dossier sur <https://app.netlify.com/drop> pour une URL publique alternative.

## 🕹️ Interaction
- **Scroll de la roulette** (ou trackpad / touch) → la caméra avance le long d'un chemin défini par 6 waypoints :
  1. Vue d'ensemble (intro)
  2. Pièce 01 — Accueil
  3. Pièce 02 — Services
  4. Pièce 03 — Réalisations
  5. Pièce 04 — Contact
  6. Recul (outro)
- **Dots de progression à droite** → cliquables pour sauter à une section.
- **Texte au-dessus de la 3D** → le hero et chaque chapitre ont leur contenu HTML qui scrolle par-dessus.

## 🏗️ Sous le capot
- **Three.js 0.166** via importmap (ESM).
- **Lenis 1.1.13** pour le smooth scroll (façon Apple/Linear).
- **Camera path** : `THREE.CatmullRomCurve3` à 6 points, sampling `getPointAt(t)` où `t = scrollProgress`.
- **2 courbes** : une pour la position de la caméra, une pour son point de regard → mouvement naturel et fluide.
- **Lerp doux** côté JS sur le `scrollT` cible → absorbe les micro-jumps si Lenis est désactivé.
- **HUD persistant** : brand top-left, dots de progression à droite, hint de scroll en bas.
- Respect `prefers-reduced-motion` (désactive Lenis, scroll natif).

## 🏠 Décor
4 pièces dans une grille 2×2, chacune avec :
- Floor + 3 murs + 3 beams de plafond.
- Strip emissive accent (couleur unique par pièce) sur le mur du fond et au sol.
- Label 3D (canvas texturé en sprite) sur le mur du fond.
- Centerpiece sur un piédestal (icosaèdre / torus knot / octaèdre / cube) qui tourne en continu.
- Ground sombre + grid décoratif + brouillon volumétrique.

## 🚀 Pour la suite
Quand le pattern est validé, on peut :
- Remplacer les centerpieces par des **vrais glTF** (mascotte volet, sandwich…) via `blender-web-pipeline` + `substance-3d-texturing`.
- Étoffer le **path** avec plus de waypoints (passages dans les murs, plongeon dans une fenêtre, zoom sur un objet…).
- Modéliser une **vraie maison Blender** complète (chambres, escalier, mezzanine).
- Ajouter des **sounds** d'ambiance par pièce (Web Audio API).
- Migrer en **React Three Fiber + Drei** si on veut composer la scène façon composants (et profiter de `<ScrollControls>` qui fait pile ça).

## 📁 Structure
```
3d-house-poc/
├─ index.html   # tout est ici (HTML + CSS + JS Three.js + Lenis)
└─ README.md    # ce fichier
```

## 🔗 Liens
- 💡 Idée d'origine : [[Idées d'évolution du système]] § *Site web entièrement en 3D*
- 🏢 [[a.SYNC Agency]] — applications possibles : siège virtuel, vitrine pôle IA
- 🥊 [[Le battant]] · 🥪 [[Beurré]] — pourraient avoir leur version 3D si pertinente

## 📝 Versions
- **2026-05-31 (soir)** — v1 : 4 pièces, navigation par clic dans la scène + boutons UI.
- **2026-05-31 (soir tard)** — v2 : **scrollytelling** — une seule page, la caméra suit une courbe Catmull-Rom le long du scroll (cette version).

## Crédits
Three.js (MIT) · Lenis (Studio Freight, MIT) · POC monté avec Claude.
