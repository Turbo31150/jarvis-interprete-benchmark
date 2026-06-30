# Analyse petaFLOP — ASUS TUF F15 vs datacenter
*2026-06-30 · specs constructeur + benchmark mesuré*

## Puissance brute de NOTRE machine (RTX 3050 Laptop 4 Go)
| Précision | Puissance | Usage |
|---|---|---|
| FP32 | **5,5 TFLOPS** | calcul général |
| FP16 (tensor) | **11 TFLOPS** (22 avec sparsité) | inférence IA |
| INT8 (tensor) | **44 TOPS** (88 avec sparsité) | **← notre Whisper (int8_float16)** |
| CPU i5-11400H | ~0,4 TFLOPS | négligeable vs GPU |

→ **Notre machine ≈ 0,011 PFLOP (FP16)**. Le benchmark FLEURS (WER 14,6 %, **19,5× temps réel**) a donc été obtenu avec **~1 % d'un petaFLOP**.

## Combien de F15 pour 1 petaFLOP (1 000 TFLOPS) ?
| Cible | Puissance FP16 | Équivalent F15 | Coût matériel |
|---|---|---|---|
| **1 PFLOP FP16** | 1 000 TFLOPS | **≈ 91 × F15** | ≈ **73 000 €** (91 × 800 €) |
| 1× NVIDIA **A100** | 312 TFLOPS | ≈ 28 × F15 | A100 ≈ 12-15 000 € |
| 1× NVIDIA **H100** | 495 TFLOPS | ≈ 45 × F15 | H100 ≈ 25-30 000 € |
| **1 PFLOP via H100** | 1 000 TFLOPS | ≈ 2 H100 | ≈ **55-60 000 €** + serveur |

## Coût par TFLOP (FP16, matériel seul)
- **F15** : 800 € / 11 = **≈ 73 €/TFLOP**
- **H100** : 30 000 € / 495 = **≈ 61 €/TFLOP**
- **A100** : 14 000 € / 312 = **≈ 45 €/TFLOP**

→ En **FLOPS bruts**, le datacenter est légèrement moins cher par TFLOP. **MAIS** ce calcul ignore : serveur + alimentation + refroidissement + ops + (en cloud) **location récurrente** (A100 ≈ 1,5-3 $/h, H100 ≈ 3-10 $/h, 24/7 = des dizaines de k€/an).

## Le vrai enseignement
1. **Pour la charge JARVIS (inférence), on n'a PAS besoin d'un petaFLOP.** 11 TFLOPS / 44 TOPS suffisent : interprète à 19,5× temps réel, **0 € marginal**.
2. La 3050 est bridée par sa **VRAM (4 Go)**, pas par ses FLOPS → le levier n'est pas « plus de petaFLOP » mais « modèle qui tient » (small/turbo).
3. **Efficience** : résultat crédible sur dataset officiel avec **~1 % d'un petaFLOP** et un matériel grand public — c'est ÇA l'argument, pas la force brute.

⚠️ FLOPS bruts ≠ perf réelle d'inférence (la bande passante mémoire et la VRAM comptent autant). Chiffres = ordre de grandeur honnête, pas un score de training.

## Sources
- [RTX 3050 Laptop specs — TechPowerUp](https://www.techpowerup.com/gpu-specs/geforce-rtx-3050-4-gb.c3744)
- [H100 FLOPS — NVIDIA](https://www.nvidia.com/en-us/data-center/h100/)
- [A100 vs H100 — Spheron](https://www.spheron.network/blog/nvidia-a100-vs-h100/)
