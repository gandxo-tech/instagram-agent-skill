## 7. Publication Instagram — contraintes réelles

- **La vidéo d'un réel publié ne peut pas être remplacée.** Tout contrôle visuel se fait avant.
- L'API refuse un fichier local (403) et les redirections (Instagram n'accepte pas les 302) : héberger le MP4 sur une URL publique directe et publier via `video_url`.
- Prévoir le poster (couverture), la légende ≤ 2 200 caractères, 3 à 5 hashtags, et la réponse aux commentaires (DM ≤ 1 000 caractères, découpé en « 1/4, 2/4… »).
- **Ne jamais publier sans accord explicite** sur le visuel et la légende.

## 8. Pipeline de rendu (mesuré)

- Python + Pillow + numpy ; ffmpeg via `imageio-ffmpeg` (`PYTHONPATH=./.pylib`, binaire dans `.pylib/imageio_ffmpeg/binaries/`). Pas de ffprobe : lire les infos avec `ffmpeg -i`.
- Frames RGB24 envoyées dans le pipe ffmpeg (`-f rawvideo -pix_fmt rgb24 -s 1080x1920 -r 30`) + WAV → H.264 High, CRF 19, AAC 48 kHz stéréo 192 kb/s, `+faststart`.
- Débit ≈ 0,1–0,2 s par frame : 900 frames ≈ 100 s. Lancer le rendu **détaché**, surveiller le log jusqu'à `ffmpeg rc 0`, ne jamais présenter le fichier avant la fin (atome `moov`).
- Mode contrôle : rendu de 4 à 6 instants clés en PNG avant le rendu complet. Vérifier : chevauchements, zones sûres, stickers, lisibilité.
- Sprites statiques dessinés une fois puis réduits en BILINEAR et recadrés ; à chaque frame, seulement coller / échelle / alpha.
