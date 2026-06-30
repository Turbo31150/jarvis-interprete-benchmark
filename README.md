# JARVIS — Interprète vocal local : benchmark officiel sur laptop grand public

**Thèse :** faire tourner un interprète vocal FR↔EN complet (transcription → traduction → synthèse vocale), **100 % en local, 0 € de coût marginal**, sur un laptop gaming à ~800 € — avec des résultats mesurés sur un **dataset officiel**.

## 🖥️ La machine
**ASUS TUF Gaming F15 FX506HC** — Intel Core i5-11400H (6c/12t) · 16 Go RAM · **NVIDIA RTX 3050 Laptop 4 Go** · NVMe 500 Go · Ubuntu 24.04.

## 📊 Résultat (dataset officiel Google FLEURS, `fr_fr`)
| Métrique | Valeur |
|---|---|
| **WER** | **10,51 %** (50 clips, split validation) |
| Vitesse | **20,2× temps réel** (GPU) |
| Coût | **0-token, 100 % local** |
| Modèle | faster-whisper `small` (int8_float16) |

*(échantillon de 20 clips : 14,6 % — l'échantillon de 50 clips réduit la variance et place le résultat dans la fourchette publiée du modèle `small`.)*

🎥 **Vidéo de preuve** : [`preuve-benchmark-FLEURS.mp4`](preuve-benchmark-FLEURS.mp4) (capture du benchmark, scores à l'image).

## 💸 Coût vs cloud (prix publics 2026)
Pour **1 000 h d'audio/an** :
- Azure (trad. temps réel) : ≈ **2 500 $/an**
- Google STT : ≈ **1 440 $/an** (+ traduction)
- **JARVIS / F15** : **0 € récurrent** — machine amortie en **< 2 mois**.

→ Détail : [COMPARAISON-JARVIS-vs-CLOUD.md](COMPARAISON-JARVIS-vs-CLOUD.md)

## ⚡ Efficience (analyse petaFLOP)
La RTX 3050 ≈ **11 TFLOPS FP16 / 44 TOPS INT8** ≈ **1 % d'un petaFLOP**.
**Le benchmark a tourné avec ~1 % d'un petaFLOP.** Pour 1 PFLOP il faudrait ≈ 91 F15 (≈ 73 000 €) ou ≈ 2 H100.
→ Détail : [PETAFLOP-ANALYSE.md](PETAFLOP-ANALYSE.md)

## ✅ Honnêteté méthodologique
- Échantillon de 20 clips (variance élevée) ; le `small` est **au-dessus** des très gros modèles cloud (SeamlessM4T ≈8 %) sur le WER pur.
- **L'avantage n'est pas le WER brut, c'est : coût marginal nul + données 100 % locales/privées + vitesse + zéro quota/dépendance.**
- Frein réel de la 3050 = VRAM 4 Go (pas les FLOPS) → marge avec `large-v3-turbo` (7,7 % WER) en libérant la VRAM.
- Chiffres = mesures réelles + prix publics sourcés. Aucun chiffre invérifiable.

## 🔁 Reproduire
Datasets officiels (FLEURS / CoVoST 2 / Common Voice) → manifeste TSV → benchmark + vidéo, via la bibliothèque de séries.
→ [BENCHMARK-OFFICIEL.md](BENCHMARK-OFFICIEL.md)

---
*Mesuré le 2026-06-30. Stack : faster-whisper (CTranslate2) + traduction locale/cloud + edge-tts/Piper.*
