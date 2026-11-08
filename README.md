# Hebrew Scam Shield 🛡️
**Adversarial synthetic data generation for robust Hebrew SMS scam detection**

HIT · Large Language Models and Applications
Team: Maor Sabatani, Opal Asraf

## Project Motivation
Israeli phones are flooded with Hebrew scam SMS messages (delayed packages, tax debts, fake banks and government services). Existing filters are trained mostly on English, and scammers constantly change their wording to evade detection.

## Problem Statement
- **Input:** a Hebrew SMS message
- **Output:** scam / legitimate + scam type (delivery, bank, government, prize, other)
- **Research question:** Does an adversarial attacker–defender loop with LLM-generated data improve the robustness of a Hebrew scam classifier?

## Visual Abstract
TBD

## Datasets Used or Collected
TBD

## Data Augmentation and Generation Methods
1. Attributed generation: scam type × impersonated entity × urgency × evasion tactic × style
2. Adversarial loop: attacker LLM rewrites caught messages; defender retrains on evading ones
3. Quality filtering: LLM judge for realism + manual review sample

## Input/Output Examples
TBD

## Models and Pipelines Used
- Baseline: GPT zero-/few-shot, multilingual zero-shot classifier
- Fine-tuned: DictaBERT / AlephBERT classifier, SetFit
- Attacker: open LLM via Ollama
- Judge: LLM-as-a-judge (realism)

## Training Process and Parameters
TBD

## Metrics
- Precision / Recall / F1 (macro and per class)
- Evasion rate per adversarial round
- Realism score (LLM judge validated against human labels)

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
