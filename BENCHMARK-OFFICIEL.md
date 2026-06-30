# Benchmarks officiels — preuve vidéo de performance

3 séries bibliothèque (version directe) :
- `bench-stt <manifest.tsv> [modele] [device]` — WER faster-whisper GPU + baselines publiées.
- `screen-record <sec> [out.mp4]` — capture écran X11 (auto-détection display).
- `bench-demo <manifest.tsv> [modele] [sec]` — **capture pendant le benchmark → vidéo partageable**.

Manifeste = lignes TSV `chemin_audio<TAB>texte_de_référence`.

## Passer aux scores OFFICIELS (datasets publics)
Pour des chiffres crédibles/comparables, utiliser un jeu de test officiel au lieu de clips maison :

| Dataset officiel | Contenu | Où |
|---|---|---|
| **FLEURS** (Google) | 102 langues, ~12 h/langue, ASR + traduction parole | HuggingFace `google/fleurs` (`fr_fr`) |
| **CoVoST 2** (Meta) | traduction parole FR↔EN | HuggingFace `facebook/covost2` |
| **Common Voice** (Mozilla) | voix réelles FR, ground-truth | commonvoice.mozilla.org |

Construire le manifeste depuis FLEURS (à faire une fois `datasets` installé) :
```bash
pip install --user --break-system-packages datasets soundfile
python3 - <<'PY'
from datasets import load_dataset; import soundfile as sf, os
ds = load_dataset("google/fleurs","fr_fr",split="test",streaming=True)
os.makedirs("/tmp/fleurs",exist_ok=True); f=open("/tmp/fleurs.tsv","w")
for i,x in zip(range(50), ds):
    p=f"/tmp/fleurs/{i}.wav"; sf.write(p, x["audio"]["array"], x["audio"]["sampling_rate"])
    f.write(f"{p}\t{x['transcription']}\n")
print("manifeste: /tmp/fleurs.tsv")
PY
~/labo/bibliotheque/lib.sh run bench-demo /tmp/fleurs.tsv small 60
```

## Défis / classements officiels (où se comparer)
- **Open ASR Leaderboard** (HuggingFace) — WER multilingue, met à jour en quasi temps réel.
- **IWSLT** (International Workshop on Spoken Language Translation) — campagne d'évaluation annuelle, tâches ASR + traduction parole.
- **WMT** — traduction (BLEU), référence DeepL/Google.

## Honnêteté méthodo (pour une vidéo crédible)
- Annoncer le **dataset exact** (FLEURS fr_fr test), le **nombre de clips**, le **modèle** et le **device** — pas de cherry-picking.
- Notre pipeline = faster-whisper (STT local GPU) + traduction cloud (Gemini/gpt-oss) ; le dire.
- La normalisation (chiffres « 8 » vs « huit ») gonfle artificiellement le WER sur les clips TTS — sur FLEURS (texte réel) c'est représentatif.

## Ce qui reste TON déclencheur (non auto-exécuté)
Publier, démarcher des influenceurs, poster sur les réseaux = actions externes irréversibles → je les prépare (vidéo, chiffres, script de post) mais **tu valides et tu publies**.
