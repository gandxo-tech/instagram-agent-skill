# Swiss Motion Graphics reel — Gandxo playbook

> **Note du 25/11/2026, à lire avant d'utiliser ce playbook.**
> Les chiffres cités plus bas (186 atteints, 401 abonnés, 46 %, 588 / 758) sont ceux de l'audit du 22/11. Les valeurs à jour sont dans `gandxo-idee-au-produit` : **402 abonnés, médiane 135 atteints, record 588 atteints / 761 vues**. Le look Swiss (papier, grille, gros type à gauche, données en filets) reste valable comme **grammaire de mise en page** d'un reel « preuve / audit », jamais comme substitut au style maison (`gandxo-reels` §1 B). Repeindre les accents en rouge `#E1141E` / bleu `#1A3FE0` si le reel doit ressembler au compte.

Recette validée pour un reel de preuve en 1080×1920. A produit « 90 jours, 3 leçons » (37,7 s, 6 scènes).

## Look

- Fond papier `#F2F0E9`, grille de 90 px à `#ECEAE2` ; encre `#0D0D10` ; accent `#FCD116` ; secondaire `#00A86B`.
- Scènes sombres (`#0B0B0F` → `#13131B`, halo chaud flouté à 190 px) pour la leçon 2 et le CTA. Alterner clair / sombre pour ponctuer.
- Marges 96 px. Repères d'angle à 46 px du bord. Filet sous l'en-tête à y 196.
- En-tête : label de section à gauche, contexte à droite, 25 px, interlettrage +2,6. Pied : handle à gauche, `0N / 06` à droite, 24 px.
- Barre de progression de 6 px en haut, largeur proportionnelle au temps global.

## Type system (Poppins)

- Titres 94–138 px Bold, alignés à gauche, interligne ~1,1, MAJUSCULES.
- Chiffres 96–290 px Bold ; unités 26–28 px, majuscules gris, interlettrage.
- Kicker 26 px Bold interlettrage +3, avec un carré d'accent de 22×22 à 40 px à sa gauche.

## Motion primitives

- Révélation de ligne par masque : rendre la ligne une fois dans une bande RGBA (base à `1.15 * size`, hauteur `1.8 * size`), puis coller seulement les rangées de la boîte de coupe en translatant avec un expo-out `1-(1-p)^4` sur 0,6 s.
- Décaler les lignes de 0,14–0,16 s ; tenir l'image complète au moins 1,2 s avant la coupe.
- Wipe de bloc couleur : rectangle qui pousse depuis son bord gauche en 0,45–0,55 s, texte dessus.
- Compteurs : la valeur évolue avec une progression adoucie sur 1,1–1,2 s.
- Filets et barres poussent depuis la gauche. Graduations seulement quand la barre est finie.
- Coupe avec un fondu de 0,14 s ; jamais plus.

## Plan de scènes (37 s)

1. Hook 5,1 s — `90 JOURS / DE DONNÉES. / 3 LEÇONS.` (troisième ligne sur un bloc d'accent).
2. Leçon 1 7,8 s — portée : compteur `186`, bloc `46 %`, filet gradué 0–401, chute `TON CONTENU FONCTIONNE. / TA PORTÉE, NON.`
3. Leçon 2 7,2 s — sombre : `588` comptes / `758` vues, flèche `401 ABONNÉS → 588 ATTEINTS`.
4. Leçon 3 6,4 s — `32 / 5 / 6`, ligne SAVES sur bloc d'accent, `LE SIGNAL LE PLUS FORT / N'EST PAS LE LIKE.`
5. Recette 5,6 s — trois lignes numérotées avec filets.
6. CTA 5,1 s — sombre : `DIAGNOSTIC ?`, bloc `PROJET`, `GANDXO`, `SITES & APPS — COTONOU`.

## Voix et son

- edge-tts `fr-FR-HenriNeural`, rate +7 %, pitch −2 Hz ; une phrase courte par scène ; conversion en WAV 48 kHz mono.
- Timing : scène = max(durée mini, voix + 0,30 s d'attaque + 0,44 s de queue).
- Lit : nappe 55 / 82,5 / 110 Hz à 0,042 de gain plus un air filtré ; impact grave et tick court à 1,65 kHz au début de chaque scène ; whoosh avant le CTA.
- Normaliser à 0,86 de pic (~ −1,3 dB max, ~ −21 dB moyen).

## Rendu

```
PYTHONPATH=./.pylib python work/render_swiss.py
```

Pipes RGB24 vers ffmpeg : libx264 crf 20, preset medium, yuv420p, AAC 192k, `+faststart`. Poster extrait avec `-ss 2.8 -frames:v 1`.

## Contrôles

- `ffmpeg -i fichier.mp4` : durée, résolution, fps, flux.
- `-af volumedetect` : pic et moyenne.
- Extraire 4 ou 5 images avec `-ss` et les regarder : collisions, débordements, zones vides. Corriger puis relancer.
