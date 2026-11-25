## 5. Faux 3D et transitions (recettes qui marchent)

**Perspective PIL** (rotation de carte en 3D, sans moteur 3D) : calculer les 8 coefficients de la transformation par résolution linéaire, puis `Image.transform(size, Image.PERSPECTIVE, coeff, Image.BICUBIC)` ; ne recoller que la boîte englobante du quadrilatère.

```python
def _coeff(pa, w, h):                      # pa = 4 coins destination, source w×h
    src = [(0,0), (w,0), (w,h), (0,h)]; A, B = [], []
    for (x, y), (u, v) in zip(pa, src):
        A.append([x, y, 1, 0, 0, 0, -u*x, -u*y]); B.append(u)
        A.append([0, 0, 0, x, y, 1, -v*x, -v*y]); B.append(v)
    try:    return np.linalg.solve(np.array(A, float), np.array(B, float)).tolist()
    except np.linalg.LinAlgError: return [1,0,0,0,1,0,0,0]
```

- **Flip** : largeur du quadrilatère × cos(π·q) (garde une largeur mini), échelle qui rétrécit puis grandit, ombrage `0,45 + 0,55·cos` pour éviter la carte « plate ».
- **Whip** : flou horizontal (3 copies décalées de 40·k), séparation RGB (±22 px), flash blanc 0,28·k, `k = sin(π·q)`.
- **Zoom-cut** : échelle 1 → 1,18 en 0,30 s + flou de mouvement léger.
- Durée de transition 0,28–0,32 s, easing smoothstep. Varier les trois, jamais deux fois la même à la suite, jamais de fondu enchaîné simple.
- Caméra globale : zoom de base 1,02–1,05 + poussée lente, pulsation au tempo, tremblement de 8 px décroissant sur les impacts.

## 6. Stickers renard (identité de marque)

**7 stickers** fournis par l'auteur, PNG détourés (296–349 px de large, liseré blanc conservé), enregistrés dans `files/stickers/fox1.png` … `fox7.png` :

| Fichier | Visuel | Sens / usage |
|---|---|---|
| fox1 | pouce levé + clin d'œil | approbation, « c'est simple » |
| fox2 | lunettes de soleil, bras croisés | maîtrise, style (le son, le visuel) |
| fox3 | pensif, bulle « ? » | question, doute, hook |
| fox4 | panneau ABONNE-TOI | CTA abonnement |
| fox5 | casque + ordinateur | travail, outils, écrire / coder |
| fox6 | mains derrière la tête, yeux fermés | « c'est réglé », sans effort |
| fox7 | bras levés, bouche ouverte | révélation, victoire, joie |

**Mapping validé du réel « liste d'outils »** : hook = fox3 · ÉCRIRE = fox5 · MONTER = fox1 · LE SON = fox2 · LE VISUEL = fox7 · VENDRE = fox6 · CTA = fox4.

- Taille 196 px de large dans les étapes, 232 au hook, 268 au CTA, rotation ±5–8°, apparition par pop (échelle 0,82 → 1, easeOutBack, 0,45 s), jamais sur un texte.
- Poser le sticker en bas à droite (x ≈ 716–742, y ≈ 1280), sous les cartes : il ne doit jamais couper un texte ni la barre de progression.
