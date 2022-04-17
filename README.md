# Yes, No or IDK: The Challenge of Unanswerable Yes/No Questions.

Data and code for the paper:
                     
                     Yes, No or IDK: The Challenge of Unanswerable Yes/No Questions
                     Elior Sulem, Jamaal Hay and Dan Roth
                     Proc. of NAACL 2022
  

## 1. Datasets

### Existing Datasets Used in the paper:

* SQuAD 2.0
  - [Train Set](https://rajpurkar.github.io/SQuAD-explorer/dataset/train-v2.0.json)
  - [Dev Set](https://rajpurkar.github.io/SQuAD-explorer/dataset/dev-v2.0.json)

* BoolQ
  - [Train Set](https://storage.cloud.google.com/boolq/train.jsonl)
  - [Dev Set](https://storage.cloud.google.com/boolq/dev.jsonl)

* MNLI 
  - [Train Set](GLUE_DATA/MNLI/train.tsv)
  - [Dev Set](GLUE_DATA/MNLI/dev_matched.tsv)

Script for downloading GLUE_DATA: https://gist.github.com/W4ngatang/60c2bdb54d156a41194446737ce03e2e

Link for MNLI (Matched) data alone: https://dl.fbaipublicfiles.com/glue/data/MNLI.zip
 
### New Datasets (released in this repository):

* BoolQ_3L: Enrichment of the BoolQ dataset with IDK questions 
  - Train Set: **DATA/BoolQ_3L/train_full.jsonl**
  - Dev Set: **DATA/BoolQ_3L/dev_full.jsonl**

* IDK portion of BoolQ_3L:
  - Train Set: **DATA/BoolQ_3L/train_IDK.jsonl**
  - Dev Set: **DATA/BoolQ_3L/dev_IDK.jsonl**

* ACE-whQA
The corpus is in SQuAD 2.0 format so it can be used with the same code.
  - Has Answer: **DATA/ACE-whQA/ACE-whQA-has-answer.json**
  - Compet. IDK: **DATA/ACE-whQA/ACE-whQA-IDK-competitive.json**
  - Non-Compet. IDK: **DATA/ACE-whQA/ACE-wkQA-non-competitive.json**

* ACE-YNQA
The corpus is in BoolQ_3L format so it can be used with the same code.
  - Full corpus: **DATA/ACE-YNQA/ACE-YNQA-full.json**
  - Has Answer: **DATA/ACE-YNQA/ACE-YNQA-has-answer.json**
  - IDK: **DATA/ACE-YNQA/ACE-YNQA-IDK.json**

* INSTRUCTIONS
The corpus is in BoolQ_3L format so it can be used with the same code.
  - Full corpus: **DATA/INSTRUCTIONS/INSTRUCTIONS-full.json**
  - Has Answer: **DATA/ACE-YNQA/INSTRUCTIONS-has-answer.json**
  
  **License:** The corpora are released under the [Creative Commons Share-Alike 3.0 license](https://creativecommons.org/licenses/by-sa/3.0/)


## 2. Code for Training and Testing on BoolQ_3L

* Environment: TensorFlow using Google Cloud and TPU (v2.8)

* Creating a virtual environment: 
                    
                    pip install virtualenv   #install virtualenv

                    cd BoolQ_3L_code
                    
                    virtualenv venv           #create environment
                    
                    source venv/bin/activate  #activate environment
                  
* Installing requirements:  
                     
                      pip install tensorflow==1.15
                      
                      pip install bert-tensorflow

                      pip install --upgrade google-api-python-client
                     
                      pip install --upgrade oauth2client
 
  
 * Downloading BERT LARGE CASED model: https://storage.googleapis.com/bert_models/2018_10_18/cased_L-24_H-1024_A-16.zip
 
   The.zip file contains three items:
   
                   A TensorFlow checkpoint (bert_model.ckpt) containing the pre-trained weights (which is actually 3 files).
      
                   A vocab file (vocab.txt) to map WordPiece to word id.
       
                   A config file (bert_config.json) which specifies the hyperparameters of the model.
                   
   It should be unzipped to some directory $BERT_MODEL.
 
 * The script **BooolQ_3L_Code/run_bert_boolq_full.py** is based on [the original BoolQ code](https://github.com/google-research/language/tree/master/language/boolq), condidering 3 labels instead of two. 
 
 Command for training and evaluating on the dev set:
 
         python  run_bert_boolq_full.py \
                --vocab_file $BERT_MODEL/vocab.txt \
                --bert_config_file $BERT_MODEL/bert_config.json \
                --init_checkpoint $BERT_MODEL/bert_model.ckpt \
                --boolq_train_data_path DATA/BoolQ_3L/train_full.json \
                --boolq_dev_data_path DATA/BoolQ_3L/dev_full.json \
                --do_train --do_eval_dev --output_dir /path/to/output-dir            
                -- use_tpu --tpu_name=$TPU_NAME --do_lower_case=False
 
 Command for testing on the out-of-domain datasets (for example ACE-whQA-competitive):
 
 $PRETRAINED_MODEL corresponds to the path to the checkpoint in the form: /path/to/output-dir/model.ckpt-1767
         
         python  run_bert_boolq_full.py \
                --vocab_file $BERT_MODEL/vocab.txt \
                --bert_config_file $BERT_MODEL/bert_config.json \
                --init_checkpoint $PRETRAINED_MODEL \
                --boolq_test_data_path DATA/ACE-whQA/ACE-whQA-IDK-competitive.json \
                --do_eval_test --output_dir /path/to/output-dir            
                -- use_tpu --tpu_name=$TPU_NAME --do_lower_case=False
                
## 3. Pretrained Models

* Extractive QA:

  - [SQuAD 2.0 baseline](https://drive.google.com/drive/folders/1AOy4vJUqmBknzgrNUR1UyLWsdgzZOEZx?usp=sharing)
  
  - [Additional pretraining on MNLI](https://drive.google.com/drive/folders/1HXrEstlj_HFvV1xJco485PReQvUvNCpk?usp=sharing)

  - [Additional pretraining on c(MNLI)](https://drive.google.com/drive/folders/1qW49KLdgI58H56vJ1FOOgyW9MnejuhSJ?usp=sharing)
  
  - [Additional pretraining on BoolQ_3L](https://drive.google.com/drive/folders/1aocDsn4GjpjWqTmf5ZhI1c6GGSlviJIV?usp=sharing)
  
* Yes/No QA with IDK:
  
  - [BoolQ_3L_baseline](https://drive.google.com/drive/folders/157IIBlF5LsuuWB4HVxpRBYq6701h_2Nq?usp=sharing)
  
  - [MNLI + BoolQ_3L](https://drive.google.com/drive/folders/1e9bFtU8umY85ZL7uXpXjlSuQ4Tyh3OLk?usp=sharing)
  
  - [c(MNLI) + BoolQ_3L](https://drive.google.com/drive/folders/1hOCy3SdFVPsuuuQ90c6058dNK5N2FsQ0?usp=sharing)
  

## 4. Commands for Training and Testing on SQuAD 2.0 and MNLI:

Code: https://github.com/google-research/bert

* MNLI: https://github.com/google-research/bert#sentence-and-sentence-pair-classification-tasks

* SQuAD 2.0: https://github.com/google-research/bert#squad-20




