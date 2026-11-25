# Mes skills (ajout personnel à ce fork)

Trois skills ajoutés à côté du pack de Jake, pour mon compte @exauce_obaguidi (Gandxo, Cotonou). Le dépôt d'origine n'est pas modifié : tout vit ici, dans ce fork.

| Dossier | Ce qu'il contient |
|---|---|
| `skills/gandxo-idee-au-produit/` | La ligne éditoriale tirée de l'audit du 25/11/2026 : le sujet « De l'idée au produit », le pitch exact, le CTA unique `PROJET`, les 5 hooks signature, la structure de reel en 22 s, le calendrier de 12 posts sur 4 semaines, le gabarit de légende, les objectifs et les garde-fous. |
| `skills/gandxo-reels/` | Le style maison (noir + grille, titre Archivo Black à double ombre rouge/bleue, pastille rouge, barre de recherche blanche, cartes à ombre bleue, stickers renard), la structure de reel qui retient, le faux 3D et les transitions, la voix off et le mix, les carrousels et stories, les contraintes réelles de publication Instagram. Détail technique dans `sound.md`, `visual.md`, `publishing.md`, `layouts.md`, `checklist.md`. |
| `skills/lemo-opuscar/` | La production vidéo par le code : brief, treatment, styles Lemo (99), rendu ffmpeg, voix off. Branché sur la ligne éditoriale ci-dessus. Playbook Swiss dans `swiss-reel-playbook.md`. |

## Ordre de chargement

1. `gandxo-idee-au-produit` — le sujet, le pitch, le CTA, les hooks.
2. `gandxo-reels` — le style et les règles de production.
3. `lemo-opuscar` — la fabrication de la vidéo.

Règle dure : Lemo fournit la méthode et les primitives de mouvement ; si un style Lemo contredit le style maison, c'est le style maison qui gagne.

## Règles qui ne bougent pas

- Rien n'est publié sans accord explicite.
- Un seul CTA par post : `PROJET`.
- Aucune métrique, aucun délai, aucun prix inventé ; KLife = concept.
- Aucune source citée, aucun signe euro.

## Installation locale

```shell
git clone https://github.com/gandxo-tech/instagram-agent-skill.git
cp -r instagram-agent-skill/skills/gandxo-* ~/.claude/skills/
cp -r instagram-agent-skill/skills/lemo-opuscar ~/.claude/skills/
```
