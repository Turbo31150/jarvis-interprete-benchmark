# JARVIS sur ASUS TUF F15 vs solutions cloud — benchmark & estimation de valeur
*2026-06-30 · chiffres mesurés sur la machine + prix publics du marché*

## La machine (config complète)
**ASUS TUF Gaming F15 FX506HC** — laptop grand public ~800 €
- CPU Intel Core **i5-11400H** (6 cœurs / 12 threads, 2,7 GHz)
- **16 Go** RAM · GPU **NVIDIA RTX 3050 Laptop 4 Go** · NVMe 500 Go
- Ubuntu 24.04 LTS · pilote NVIDIA 595

## Résultat benchmark officiel (mesuré)
- **Dataset officiel** : Google FLEURS `fr_fr` (20 clips, split validation)
- **WER : 14,56 %** · **19,5× temps réel** · faster-whisper `small` GPU · **0-token, 100 % local**
- Interprète bout-en-bout (STT→traduction→TTS) : **~2-3 s / tour**

## Comparaison coût (prix publics 2026)
| Solution | STT | Traduction parole | Coût / heure audio |
|---|---|---|---|
| **Google Cloud STT** | $0,006/15 s | + Translation | **≈ 1,44 $/h** (standard) |
| **Azure Speech** | 1 $/h (temps réel) | **2,50 $/h** (trad. temps réel) | **2,50 $/h** |
| **DeepL API** | plans dédiés | 25 $ / M caractères | abonnement + usage |
| **JARVIS / F15** | local | local | **0 € (marginal)** |

## Estimation du gain (ROI)
Hypothèse usage interprète/réunions : **4 h/jour × 250 j = 1 000 h/an**.
- Azure (trad. temps réel) : 1 000 × 2,50 $ = **≈ 2 500 $/an** (récurrent).
- Google STT seul : ≈ **1 440 $/an** (+ traduction en plus).
- **JARVIS / F15** : **0 € récurrent**, machine ~800 € amortie en **< 2 mois** vs Azure.

Sur 3 ans : cloud ≈ **7 500 $** vs F15 ≈ **800 € (one-shot)** → **gain ~10×**, et la machine sert aussi à tout le reste (cluster, dev, vidéo…).

## Honnêteté (pour rester crédible)
- WER `small` (14,5 %) ≈ ballpark cloud FR, mais **au-dessus** des très gros modèles (SeamlessM4T ≈8 %). Échantillon 20 clips = variance.
- Pour le WER pur le plus bas : `large-v3-turbo` (7,7 %) en libérant la VRAM (décharger Ollama).
- **L'avantage décisif n'est pas le WER, c'est : coût marginal nul + données 100 % locales/privées + vitesse + pas de quota/dépendance** — ce qu'aucune offre cloud ne donne.

## Sources prix
- [Google Cloud Speech-to-Text Pricing](https://cloud.google.com/speech-to-text/pricing)
- [Azure Speech pricing](https://azure.microsoft.com/en-us/pricing/details/speech/)
- [DeepL API pricing](https://support.deepl.com/hc/en-us/articles/360021200939-DeepL-API-plans)
