# 3D House — POC navigation pièce-par-pièce

Proof of concept d'un site web entièrement en 3D où **chaque pièce = une page**. Idée d'Herman, capturée dans le cerveau ([[Idées d'évolution du système]] § *Site web entièrement en 3D*).

> 🥊 Pattern type **Awwwards / Bruno Simon / Active Theory**, mais minimal et **single-file** pour valider le concept avant d'investir.

## 🎮 Comment tester

**Option la plus simple** : **double-clique sur `index.html`** → ça s'ouvre dans ton navigateur, ça marche tout de suite (Three.js chargé depuis CDN unpkg, aucune install nécessaire).

Sinon :
- Glisse-dépose le dossier sur <https://app.netlify.com/drop> → URL publique en 10 sec.
- Ou `python -m http.server` dans le dossier puis `http://localhost:8000`.

## 🕹️ Commandes
- **Clic sur une pièce** dans la scène 3D → la caméra y va.
- **Boutons en haut à droite** → idem, par nom de pièce.
- **Touches 1-4** au clavier → raccourci pour les 4 pièces.

## 🏗️ Ce qu'il y a sous le capot
- **Three.js 0.166** chargé via importmap depuis unpkg (zéro build).
- 4 pièces dans une grille 2×2 (Accueil · Services · Réalisations · Contact).
- Caméra qui voyage entre les pièces en arc (courbe de Bézier quadratique), easing in-out cubic.
- Sprites texturés pour les labels 3D.
- Pièce centrale (icosaèdre / torus knot / octaèdre / cube) qui tourne sur un piédestal.
- Strip emissive sur le mur du fond, beams au plafond, sols texturés.
- Lights : ambient + directional avec shadows + rim light rouge.
- Mini-map en bas à droite (canvas 2D).
- HUD responsive, respect `prefers-reduced-motion`.

## 🚀 Pour passer en POC sérieux (vrais assets)
Quand tu seras prêt à investir :
- 🏗️ **`blender-web-pipeline`** — modélise une vraie maison dans Blender, export glTF Draco.
- 🎨 **`substance-3d-texturing`** — textures PBR (bois, métal, tissu).
- 🎥 **`cinematique-scroll-recettes`** — recette « 3D camera scroll path » pour un voyage cinématique plus poussé.
- 🌊 **`react-spring-physics`** — si tu passes sur React Three Fiber, des springs pour des mouvements ultra-naturels.
- ✨ **`animations-awwwards-premium`** — couche GSAP/Lenis par-dessus pour le niveau Awwwards.

## 📁 Structure
```
3d-house-poc/
├─ index.html   # tout est ici (HTML + CSS + JS Three.js)
└─ README.md    # ce fichier
```

## 🧪 Variantes faciles à tester depuis ce POC
- Changer le contenu / nombre de pièces : edit l'array `ROOMS` en haut du script (~10 lignes).
- Changer la palette : variables CSS au début (`--rouge`, `--vert-volet`, `--vert-deep`, `--creme`, `--noir`).
- Remplacer les centerpieces par des **vrais glTF** (chaise, machine à café, mascotte Le battant…) : `new GLTFLoader().load(url, gltf => grp.add(gltf.scene))`.
- Ajouter des **sons d'ambiance** par pièce (Web Audio API).
- Mode **first-person** (WASD + souris) au lieu de teleport-by-click.

## 🔗 Lien avec le reste
- 💡 Idée d'origine : [[Idées d'évolution du système]] § Site web entièrement en 3D
- 🏢 [[a.SYNC Agency]] — applications possibles : siège virtuel, vitrine pôle IA
- 🥊 [[Le battant]] — atelier 3D si validé
- 🥪 [[Beurré]] — boutique vintage 3D si validé

## 📝 Crédits
Three.js (MIT) · POC monté le 2026-05-31 par Claude avec Herman.
