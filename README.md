# SMIT

This repository contains the implementation of **SMIT (Small Model for Intent Translation)**.  
It includes model execution, training, and evaluation pipelines based on **Phi-3.5 using NLLB-200** and **NLLB-200 fine-tuned with QLoRA**, as well as a structured dataset divided into **training**, **evaluation**, and **test** splits to ensure reproducibility and fair assessment.

The project is designed to study efficient intent translation using small and parameter-efficient language models while maintaining semantic correctness and task fulfillment.

---

## Repository Structure

SMIT/
├── Dataset/
│ ├── train/
│ ├── evaluation/
│ └── test/
├── models/
├── notebooks/
├── scripts/



---

## Dataset

The dataset is organized into three disjoint partitions:

- **train/**  
  Used for fine-tuning the models.

- **evaluation/**  
  Used during training for validation and hyperparameter selection.

- **test/**  
  Used exclusively for final evaluation and reporting results.

All splits share the same data format to ensure consistency across experiments.  
The dataset is intended for intent translation tasks, where inputs are expressed in natural language and outputs follow a standardized intent representation.

---

## Models

This repository supports the following model configurations:

### Phi-3.5 (NLLB-200)

A baseline configuration based on **Phi-3.5** using the **NLLB-200** architecture.  
This model is used to establish a reference performance for multilingual and intent translation tasks.

### NLLB-200 + QLoRA

A parameter-efficient fine-tuned version of NLLB-200 using **QLoRA**.  
This approach significantly reduces memory and computational requirements while maintaining competitive performance, making it suitable for resource-constrained environments.

---

## Requirements

To install the required dependencies, run:

```bash
pip install -r requirements.txt


python run_phi3_5.py \
  --model_name_or_path <model_path_or_name> \
  --input_file input.json \
  --output_file output.json


python run_nllb200_qlora.py \
  --model_name_or_path <model_path_or_name> \
  --input_file input.json \
  --output_file output.json

python train_nllb200_qlora.py \
  --train_data Dataset/train \
  --eval_data Dataset/evaluation \
  --output_dir models/nllb200_qlora_finetuned

python eval.py \
  --model_dir models/nllb200_qlora_finetuned \
  --test_data Dataset/test
