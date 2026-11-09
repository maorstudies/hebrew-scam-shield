# ScamLoop-HE 🛡️
**Attacker-defender training for robust Hebrew SMS phishing (smishing) detection**

HIT · Large Language Models and Applications

Team: Maor Sabatani, Opal Asraf

## Project Motivation
Israeli phones receive a steady stream of Hebrew scam SMS messages (delayed packages, tax debts, fake banks and government services). We found no public labeled Hebrew scam SMS dataset, existing multilingual spam sets are machine-translated and skip Hebrew, and scammers constantly change their wording to evade detection.

## Problem Statement
- **Input:** a Hebrew SMS message
- **Output:** scam / legitimate + scam type (delivery, bank, government, prize, other)
- **Research question:** Does an iterative attacker-defender loop on native Hebrew data detect real and never-seen SMS phishing (smishing) campaigns better than training on translated English data?

## Visual Abstract
TBD

## Datasets Used or Collected
- Synthetic Hebrew scams (~2,000) + adversarial rounds
- Synthetic legitimate look-alikes (~2,000), e.g. bank or HMO notices with official .co.il / .gov.il links
- Real test set: 150 messages (75 scam + 75 legit), manually labeled
- Translated English smishing data (baseline)

## Data Augmentation and Generation Methods
1. Attributed generation: label and attributes are sampled first (scam type × impersonated entity × urgency × evasion tactic × style), then an LLM writes the message
2. Attacker-defender loop: attacker LLM rewrites caught messages; defender retrains on evading ones plus a replay buffer of all earlier rounds
3. Quality filtering: LLM judge for realism + manual review sample

## Input/Output Examples
TBD

## Models and Pipelines Used
- Baselines: GPT zero-/few-shot; classifier trained on translated English data
- Defenders (fine-tuned): DictaBERT / AlephBERT (Hebrew BERT models), SetFit
- Attacker: open LLM run locally (Ollama) + GPT via API
- Judge: LLM-as-a-judge (realism)

## Training Process and Parameters
TBD

## Metrics
- Precision / Recall / F1 (macro and per class) on real messages and on a scam type held out from training
- Evasion rate per adversarial round (loop stops below 5% or after 5 rounds)
- Realism score (LLM judge validated against human labels, Cohen's kappa)
- SHAP explanations of misclassified messages

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
