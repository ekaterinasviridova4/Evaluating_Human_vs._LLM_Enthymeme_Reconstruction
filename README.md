# Overview

This repository contains the implementation details of the paper "Better than the Gold Standard? Evaluating Human vs. LLM Enthymeme Reconstruction in Natural Language Argumentation".
This work focuses on reconstructing implicit premises and claims in argumentative texts, using different families of generative models and zero-shot prompting. 
Human reconstructed data is stored in [data/dialogue/out_dial_jsonl](data/dialogue/out_dial_jsonl).

## Data Structure

The data is organized into Dialogue-structured (speaker separated) texts including raw (non-annotated) and human-annotated CMV text: 

- [data/dialogue/out_dial_jsonl](data/dialogue/out_dial_jsonl): Dialogue dataset with Implicit/Explicit annotations ([train_labeled.jsonl](data/dialogue/out_dial_jsonl/train_labeled.jsonl), [dev_labeled.jsonl](data/dialogue/out_dial_jsonl/dev_labeled.jsonl), [test_labeled.jsonl](data/dialogue/out_dial_jsonl/test_labeled.jsonl)); Human-reconstructed gold-standard data ([post_processed_train.jsonl](data/dialogue/out_dial_jsonl/post_processed_train.jsonl), [post_processed_dev.jsonl](data/dialogue/out_dial_jsonl/post_processed_dev.jsonl), [post_processed_test.jsonl](data/dialogue/out_dial_jsonl/post_processed_test.jsonl))
- [data/dialogue/out_dial_fine_grained_jsonl](data/dialogue/out_dial_fine_grained_jsonl): Dialogue dataset with fine-grained annotations.
- [data/dialogue/out_dial_premise_claim_jsonl](data/dialogue/out_dial_premise_claim_jsonl): Dialogue dataset with premise and claim annotations.


---

## Reconstruction & Evaluation

Scripts located in [scripts/generation](scripts/generation) used to reconstruct implicit information.
- [scripts/generation/ann_full_gen_gemini.py](scripts/generation/ann_full_gen_gemini.py): Full dialogue generation script using Gemini/GPT models.
- [scripts/generation/ann_short_gen_gemini.py](scripts/generation/ann_short_gen_gemini.py): Speaker exchange generation script using Gemini/GPT models.
- [scripts/generation/ann_full_gen_mistral24.py](scripts/generation/ann_full_gen_mistral24.py): Full dialogue generation script using Mistral/OLMo models.
- [scripts/generation/ann_short_gen_mistral24.py](scripts/generation/ann_short_gen_mistral24.py): Speaker exchange generation script using Mistral/OLMo models.

Scripts located in [scripts/evaluation](scripts/evaluation) used to evaluate automatic reconstruction against human gold-standard reconstruction.
- Fulltext scripts: evaluation of complete reconstructions with BLEU, ROUGE and SBERT.
- Associations scripts: evaluation of reconstruction pairs with BLEU, ROUGE and SBERT.

---

## Data Processing Tools

### Files for breaking down and re-joining dialogues (speaker exchanges)
Tools located in [scripts/processing](scripts/processing) for splitting dialogues into speaker exchanges and joining back the reconstructions.
- [scripts/processing/extract_speaker_exchanges.py](scripts/processing/extract_speaker_exchanges.py): Splits dialogues into N-turn exchanges.
- [scripts/processing/join_reconstructed_exchanges.py](scripts/processing/join_reconstructed_exchanges.py): Merges reconstructions of exchanges back into full dialogues.

---

## Configuration

Configuration files for job submission (OAR scheduler) are located in [configs](configs).
- [configs/oar_config.sh](configs/oar_config.sh): Config for Mistral/OLMo generation.
- [configs/oar_config_litellm.sh](configs/oar_config_litellm.sh): Config for LiteLLM (Gemini/GPT) generation.

---
## Evaluation Guidelines

Complete guidelines for the human evaluation study are available in [Evaluation_Guidelines.pdf](Evaluation_Guidelines.pdf).

---

## Results Structure

The results are divided into [results_dev/](results_dev) and [results_test/](results_test), containing:
- `ann_full_reconstructed_*`: Full dialogue reconstructions.
- `ann_short_reconstructed_*`: Speaker exchange reconstructions.
- `joined_reconstructed/`: Merged outputs from exchange reconstructions.
- `evaluation_results/`: BLEU, ROUGE, and SBERT metrics.

---

## Installation
```bash
# General dependencies
pip install -r requirements.txt

# For API-based reconstruction (LiteLLM)
pip install -r requirements_litellm.txt

# For evaluation metrics
pip install -r scripts/evaluation/requirements_fulltext_bleu.txt
pip install -r scripts/evaluation/requirements_fulltext_rouge.txt
pip install -r scripts/evaluation/requirements_fulltext_sbert.txt
```
---

## Cite Us

```bibtex
@inproceedings{sviridova2026better,
  author    = {Sviridova, Ekaterina and Cabrio, Elena and Villata, Serena},
  title     = {Better than the Gold Standard? {E}valuating Human vs. {LLM} Enthymeme Reconstruction in Natural Language Argumentation},
  booktitle = {Proceedings of the 11th International Conference on Computational Models of Argument (COMMA 2026)},
  year      = {2026},
  note      = {To appear}
}
```

