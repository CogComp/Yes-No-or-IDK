# Do We Know What We Don't Know? Studying Unanswerable Questions across Different Formats and Domains

## 1. Datasets

### Existing Datasets Used in the paper:

* SQuAD 2.0
 - Train Set: https://rajpurkar.github.io/SQuAD-explorer/dataset/train-v2.0.json
 - Dev Set: https://rajpurkar.github.io/SQuAD-explorer/dataset/dev-v2.0.json

* BoolQ
 - Train Set: https://storage.cloud.google.com/boolq/train.jsonl
 - Dev Set: https://storage.cloud.google.com/boolq/dev.jsonl

* MNLI 
- Train Set: GLUE_DATA/MNLI/train.tsv
- Dev Set: GLUE_DATA/MNLI/dev_matched.tsv
Script for downloading GLUE_DATA: https://gist.github.com/W4ngatang/60c2bdb54d156a41194446737ce03e2e
Link for MNLI (Matched) data alone: https://dl.fbaipublicfiles.com/glue/data/MNLI.zip
 
### New Datasets (released in this repository):

* BoolQ_3L: Enrichment of the BoolQ dataset with IDK questions 
- Train Set: DATA/BoolQ_3L/train_full.jsonl
- Dev Set: DATA/BoolQ_3L/dev_full.jsonl

* IDK portion of BoolQ_3L:
- Train Set: DATA/BoolQ_3L/train_IDK.jsonl
- Dev Set: DATA/BoolQ_3L/dev_IDK.jsonl

* ACE-whQA
The corpus is in SQuAD 2.0 format so it can be used with the same code.
- Has Answer: DATA/ACE-whQA/ACE-whQA-has-answer.json
- Compet. IDK: DATA/ACE-whQA/ACE-whQA-IDK-competitive.json
- Non-Compet. IDK: DATA/ACE-whQA/ACE-wkQA-non-competitive.json

* ACE-YNQA
The corpus is in BoolQ_3L format so it can be used with the same code.
- Full corpus: DATA/ACE-YNQA/ACE-YNQA-full.json
- Has Answer: DATA/ACE-YNQA/ACE-YNQA-has-answer.json
- Compet. IDK: DATA/ACE-YNQA/ACE-YNQA-IDK.json

* INSTRUCTIONS
The corpus is in BoolQ_3L format so it can be used with the same code.



## 2. Code for Training and Testing on BoolQ_{3L}

## 3. Pretrained Models

## 4. Commands for Training and Testing the Models (Including Hyperparameters)


