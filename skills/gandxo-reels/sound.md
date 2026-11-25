## 4. Voix off et son

- `edge-tts`, voix `fr-FR-HenriNeural`, `rate=+12%`, un fichier par scène, durées mesurées puis scènes calées dessus.
- Musique synthétisée : 112 BPM, kick + hats + basse, impacts sur les transitions, riser avant le CTA, sub-drop sur le CTA, whooshes discrets (×0,18) 0,3 s avant chaque transition.
- **Ducking** de la musique sous la voix off (−6 à −9 dB pendant la parole), remontée dans les respirations.
- Niveaux livrés : pic ≤ −0,5 dB, moyenne ≈ −19 dB ; encodage `-af loudnorm=I=-14:TP=-1.5:LRA=11`. Vérifier avec `volumedetect` : un pic à 0 dB est refusé.
