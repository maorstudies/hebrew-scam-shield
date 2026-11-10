# ScamLoop-HE 🛡️
**Attacker-defender training for robust Hebrew SMS phishing (smishing) detection**

HIT · Large Language Models and Applications

Team: Maor Sabatani, Opal Asraf

## Project Motivation
Israeli phones receive a steady stream of Hebrew scam SMS messages (delayed packages, tax debts, fake banks and government services). We found no public labeled Hebrew smishing dataset (searched Hugging Face, Kaggle, arXiv and Hebrew NLP resource lists, Nov 2026); existing multilingual spam sets are machine-translated and skip Hebrew. Scammers also keep rewording to evade filters.

## Problem Statement
- **Input:** a Hebrew SMS message
- **Output:** scam / legitimate (main) + scam type: delivery, bank, government, prize, other (secondary)
- **Research question:** Does iterative adversarial training on synthetic Hebrew SMS data improve smishing detection on independently collected real Hebrew messages, compared with native-Hebrew training alone and a translated-English baseline?
- **Secondary question:** Does it also catch a scam type held out from training?

## Related Work
| Work | What they did | Gap |
|---|---|---|
| Scam Shield (Chang et al., 2025) | LLM rewrites scams to look legit; one fine-tuning pass (English) | No iterative retraining |
| Adversarial Robustness in Smishing Detection (arXiv 2608.12889) | Evasive SMS made with Gemini to attack classifiers (English, Swahili) | Retraining left as future work |
| COVA (arXiv 2604.11752) | Attacker and victim LLM agents generate scam dialogues (English) | No detector in the loop |
| SMS Spam Multilingual Collection | Spam SMS machine-translated to 21 languages | No Hebrew |

## Visual Abstract
TBD

## Datasets Used or Collected
- Synthetic Hebrew scams: 2,000 base + up to 1,000 from adversarial rounds (5 × 200)
- Synthetic legitimate look-alikes: 2,000 (legitimacy defined by verified sender, not by domain)
- Real test set (target, to be collected): 150 messages (75 scam + 75 legit), labeled separately by both team members; personal details removed
- Translated English smishing data (baseline)

## Data Augmentation and Generation Methods
1. Attributed generation: label and attributes are sampled first (scam type × impersonated entity × urgency × evasion tactic × style), then an LLM writes the message
2. Attacker-defender loop: each round the attacker rewrites 200 caught scams; a message evades if the defender labels it legitimate; the defender retrains on evading messages plus a replay buffer of earlier rounds
3. Quality control: LLM judge for realism + hand-checked sample for realism and label correctness

## Experimental Design
Same defender (DictaBERT) and same real test set in all conditions:
1. Translated English (baseline)
2. Native Hebrew synthetic only
3. Native + static attacker data (generated in advance)
4. Native + attacker loop (ours)

Conditions 3 and 4 receive the same amount of attacker data, so the only difference is adaptive feedback.

**Leakage control:** train/val/test split by generation template; near-duplicates removed; the real test set is never used for training or model selection.

## Input/Output Examples
TBD

## Models and Pipelines Used
- Defender: DictaBERT (main); SetFit only if time allows
- Baselines: DictaBERT trained on translated English data; GPT few-shot for reference
- Attacker: open LLM run locally (Ollama) + GPT via API
- Judge: LLM-as-a-judge

## Training Process and Parameters
TBD

## Metrics
- Precision / Recall / F1 on the real test set (main) and on a held-out scam type (secondary)
- Evasion rate: % of the 200 new attacker scams per round labeled legitimate (loop stops below 5% or after 5 rounds)
- Realism: LLM judge and human sample; Cohen's kappa for judge-human agreement
- SHAP for error analysis

## Results
TBD

## Repository Structure
- slides/ - presentations (PPT + PDF)
- code/ - Python files and notebooks
- data/ - generated and collected data (JSON / CSV)
- results/ - experiment results
- visuals/ - figures and visual abstract

## Team Members
- Maor Sabatani
- Opal Asraf
