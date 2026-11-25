---
name: lemo-opuscar
description: >-
  Create motion-design videos and vertical reels as code using the Lemo-Opuscar
  workflow: 99 named visual styles, brief-to-render pipeline, and
  ffmpeg/voiceover finishing, wired to Gandxo's active editorial line
  ("De l'idée au produit", pitch, hooks, PROJET CTA). Use when the user wants a
  reel, an animated explainer or a motion-design video produced by writing code
  rather than with a generative video model.
---

# Lemo-Opuscar (adapté pour Gandxo)

À utiliser pour créer des vidéos motion-design, des explainers animés ou des reels verticaux en écrivant du code (pas de modèle vidéo génératif). Source : le fork Lemo-Opuscar de Gandxo (fork de lemomo-ai/lemo-opuscar).

## 0. Ce skill ne choisit pas le sujet

Le sujet, le pitch, les hooks, le CTA et le calendrier viennent de **`gandxo-idee-au-produit`** (ligne active : « De l'idée au produit »). Le style vient de **`gandxo-reels`**.

Ordre de chargement obligatoire : `gandxo-idee-au-produit` → `gandxo-reels` → ce skill.
Lemo fournit la **méthode de production** (brief, treatment, rendu, mix, vérification) et une bibliothèque de **primitives de mouvement**. Il ne remplace jamais la palette, la typographie ni les composants maison.

Règle dure : **si un style Lemo contredit le style maison, c'est le style maison qui gagne.** Un « Swiss » ou un « Dark Tech » ne s'utilise que pour ses primitives (masques de lignes, compteurs, barres qui poussent, coupes courtes), repeintes avec les couleurs et les composants de `gandxo-reels`.

## Core idea

- Lemo-Opuscar makes films as code: pick a style, write a treatment/shot plan, implement scenes in code, render frames, then assemble with ffmpeg and add voice/music/mix.
- 99 styles, 15 categories. Each style has a `STYLE.md` (look, motion, typography, color, do/don't) and a demo. Styles marked with a star need an image generator for key assets; prefer non-star or asset-light styles when speed matters.

## Workflow

1. **Brief** — tiré de la ligne éditoriale, pas inventé : quel post du calendrier, quel pilier (preuve / transformation / comment), quel hook parmi les cinq, format, durée, CTA `PROJET`.
2. **Treatment** — scène par scène : durée, texte à l'écran, voix off, visuel / action, transition.
3. **Style frame** — appliquer d'abord le style maison, puis emprunter des primitives à un style Lemo. Vérifier une image de contrôle contre un vrai post avant de produire.
4. **Production** — implémenter les scènes en code (Python / PIL ou la stack du projet), rendu 1080×1920.
5. **Voix et mix** — voix off naturelle, générée avec edge-tts (français), mix voix / musique / SFX, niveaux vérifiés.
6. **Vérification** — durée, résolution, fps, audio présent, lisibilité, marges sûres, orthographe, chiffres réels. MP4 + poster.
7. **Livraison** — ne jamais publier, DM ou envoyer sans validation explicite de l'utilisateur.

## Adaptation Gandxo (valeurs à jour, 25/11/2026)

- **Format** : 1080×1920, 30 fps, H.264 + AAC, **15 à 22 s** (le calendrier ne dépasse pas 22 s ; 30–40 s uniquement sur demande explicite). ≤ 15 Mo.
- **Marque** : noir (5,5,10) + grille fine, rouge `#E1141E`, bleu `#1A3FE0`, blanc pur. Titres **Archivo Black** MAJUSCULES à double ombre dure (rouge 0,055 × taille, extrusion bleue 0,11 × taille) ; Poppins Bold/Regular pour le reste. Pastille rouge de sur-titre, barre de recherche blanche à ombre bleue + badge rond rouge, cartes sombres à ombre bleue pleine, stickers renard. **Jamais de fond bleu nuit dégradé**, jamais de dégradés mous, jamais de jaune ni de violet. Les anciennes palettes `#FCD116` et `#00A86B` sont abandonnées.
- **Structure** : hook → problème vécu → preuve à l'écran → la main / le code → bloc rouge + `PROJET`. Une idée par écran.
- **Chiffres réels uniquement** : 402 abonnés, médiane 135 atteints, record 588 atteints / 761 vues (11/10), 36 likes / 18 commentaires / 50 % d'engagement / 20,5 s de visionnage (18/09). Jamais de métrique, de délai ou de prix inventé. KLife = concept.
- **Voix** : `fr-FR-HenriNeural`, pitch −2 Hz, `rate` +7 % sur un reel « preuve » posé, jusqu'à +12 % sur un reel rythmé ; une phrase courte par scène (~3,4 s max).
- **CTA** : un seul, écrit **et** dit — « Commente PROJET. » Jamais LIENS / PORTFOLIO / SITES en parallèle. Pas de logo final muet.
- **Publication** : jamais sans accord explicite ; la vidéo d'un reel publié n'est pas remplaçable.

## Style selection (par pilier, pas par nouveauté)

- **Preuve / produit à l'écran** → style maison + primitives « Dark Tech Keynote » pour les transitions. C'est le cœur de la série.
- **Transformation / avant-après** → primitives de « Kinetic Typography » (masques de lignes, compteurs) repeintes en maison.
- **Audit, chiffres, leçons** → « Swiss Motion Graphics » (grille, gros type à gauche, données en filets), playbook dans `swiss-reel-playbook.md`, uniquement comme grammaire de mise en page.
- **Hook ultra-court** → « Neon Tubes » seulement pour l'énergie du mouvement, jamais pour les couleurs.
- Jamais deux grammaires de mouvement dans le même reel.

## Technical notes

- ffmpeg via `imageio_ffmpeg` (`.pylib/imageio_ffmpeg/binaries/ffmpeg-linux-x86_64-v9.0.2`), lancé avec `PYTHONPATH=./.pylib`. Pas de ffprobe système : inspecter avec `ffmpeg -i` et `-af volumedetect`.
- Rendu en pipes de frames RGB24 vers ffmpeg (libx264, crf 19–20, yuv420p, `+faststart`), audio mixé en numpy et écrit en WAV 48 kHz stéréo.
- Cible audio : pic ≤ −0,5 dB (viser −1,5 dB), moyenne autour de −19 / −20 dB ; `loudnorm=I=-14:TP=-1.5:LRA=11` à l'encodage.
- Rendu détaché, on ne présente jamais le fichier avant `ffmpeg rc 0`.
- Mettre en cache textes et sprites : le dessin de texte PIL par frame est le premier poste de coût ; recadrer chaque sprite sur sa boîte englobante.

## Quality bar

- Mobile-first : titres 90–140 px, contraste AAA, marges 88 px (reel) / 96 px (Swiss), zone sûre y 250→1570.
- Le mouvement sert le message ; un accent par scène ; le rouge ne porte qu'un mot ou un chiffre.
- Un changement visuel toutes les 1,5 à 2,5 s, jamais plus de 3 s sans mouvement.
- Livrer le MP4, le poster PNG, la légende (gabarit de `gandxo-idee-au-produit`), et dire ce qui a été vérifié ou non.
