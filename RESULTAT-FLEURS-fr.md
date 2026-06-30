# Résultat benchmark officiel — FLEURS fr (Google)

- **Dataset** : google/fleurs, config `fr_fr`, split validation, **20 clips** (lecture directe parquet en cache).
- **Modèle** : faster-whisper `small`, GPU RTX 3050, int8_float16.
- **WER GLOBAL : 14,56 %** · **19,5× temps réel** · 0-token, 100% local.
- Vidéo de preuve : `~/Vidéos/bench-small-20260630-061726.mp4`

## Lecture honnête
- `small` (le modèle qui tient dans 4 Go partagés avec Ollama) → ~14,5 % sur 20 clips : crédible mais **au-dessus** des gros modèles (SeamlessM4T ≈8 %, turbo 7,7 %). Échantillon petit = variance élevée ; une partie des "erreurs" = noms propres + ponctuation ajoutée par Whisper.
- **Là où on gagne vraiment** : vitesse (19,5× temps réel), **0-token**, **local/privé**, et l'**interprète bout-en-bout** (STT+trad+TTS en 2-3 s) — ce que DeepL/Microsoft (cloud, payant) ne font pas.
- Pour battre les gros sur le WER pur : charger `large-v3-turbo` (7,7 %) en libérant la VRAM (décharger Ollama). Toggle prêt.
