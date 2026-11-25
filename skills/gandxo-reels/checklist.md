## 10. Checklist avant de livrer

1. Première image compréhensible sans le son. 2. Aucun texte sous la pastille, la progression ou l'UI Instagram. 3. Aucun euro, aucune mention de source. 4. Orthographe et accents vérifiés à l'image. 5. Noms et domaines exacts. 6. Stickers à leur place, aucun recouvrement. 7. Pic audio ≤ −0,5 dB, aucune voix coupée. 8. Durée annoncée = durée réelle. 9. Poster exporté avec la vidéo. 10. Poids ≤ 15 Mo pour la data mobile. 11. **Le style vérifié sur une image contre ses vrais posts**. 12. Un seul CTA, et c'est `PROJET`.

## 11. Pièges connus (accumulés par l'expérience)

- **Erreur majeure déjà commise** : livrer un reel en bleu nuit dégradé avec grosses cartes bleu vif, puis s'entendre dire « c'est pas mon style ». Son style, c'est `SKILL.md` §1 B. Vérifier une image de référence avant de produire.
- Un glyphe absent de la police sort en carré vide : dessiner les flèches en primitives.
- Un easing trop agressif (easeOutBack) sur les cartes 3D casse la lisibilité : smoothstep pour la caméra et les cartes.
- Une carte collée sans son canal alpha pendant un flip devient un rectangle noir : toujours coller avec masque.
- La normalisation audio faussée par le padding des WAV : mesurer après le mix final.
- Les titres trop hauts passent sous la pastille dès que la caméra zoome : titre à y 378 minimum.
- Un bloc rouge collé trop haut coupe l'ombre du titre au-dessus : laisser 14 px.
- Un sprite pleine largeur avec peu de contenu ralentit tout : recadrer sur la boîte englobante.
- Le zoom laissé actif après une coupe : borner dans le temps et revenir à 1.
- `from module import *` n'importe pas les noms en `_`.
- Le DM Instagram est limité (~1 000 caractères) ; légende 2 200 maximum.
- Les vieux MP4 livrés sont écrasés sans copie : garder une copie dans `work/` avant un nouveau rendu.
- Les URL signées du CDN Instagram exigent **tous** leurs paramètres, sinon « URL signature mismatch ».
- Deux posts le même soir se cannibalisent (24/11 : 16 atteints, 85 % de skip).

## 12. Workflow d'un agent

1. **Cadrer** (≤ 1 question) : quel post du calendrier, format, durée, musique éventuelle. Intention claire = produire.
2. **Vérifier les faits** et les chiffres cités (existence, gratuit / payant, limites, métriques relues dans les stats).
3. **Écrire** : hook (un des cinq, ou même famille), 1 idée par écran, puces ≤ 42 caractères, « À SAVOIR » honnête, légende, DM.
4. **Produire** : planche-contact, validation des zones et du style, rendu complet détaché, contrôle `ffmpeg -i` + `volumedetect` + poster.
5. **Livrer** : MP4 + poster, en 3 à 6 lignes de texte simple, sans jargon, avec une seule suite proposée. Rien n'est publié avant accord.
