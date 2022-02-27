# T5 on Table-To-Text Generation: ToTTo
Table-To-Text Generation using T5 (on ToTTo Dataset).<br/>
I have referenced the following papers:
* ToTTo: A Controlled Table-To-Text Generation Dataset ([Parikh et al.](https://arxiv.org/abs/2004.14373), 2020, [Github](https://github.com/google-research-datasets/ToTTo))
* Text-to-Text Pre-Training for Data-to-Text Tasks ([Kale and Rastogi](https://arxiv.org/abs/2005.10433), 2020)
## Usage
### Clone This Repo
```bash
git clone https://github.com/ChainsmokersAI/T5-on-ToTTo.git
cd T5-on-ToTTo/
mkdir model
```
### Get Dataset
```bash
wget https://storage.googleapis.com/totto-public/totto_data.zip
unzip totto_data.zip
```
### Get (Official) Evaluation Codes
```bash
git clone https://github.com/google-research/language.git language_repo
cd language_repo
pip install -r language/totto/eval_requirements.txt

# Evaluation Codes DO NOT Work with Recent Version of 'sacrebleu'
pip uninstall sacrebleu
pip install sacrebleu==1.5.1

# Run Sample (Jupyter) Codes
```
### Sample Codes
* Preprocess ([code](https://github.com/ChainsmokersAI/T5-on-ToTTo/blob/main/Preprocess.ipynb))
* Fine-Tune (Not Multi-Task Learner) T5 Only Using Subtable  ([code](https://github.com/ChainsmokersAI/T5-on-ToTTo/blob/main/(Subtable)%20Finetune.ipynb))
* Generation & Evaluation on Dev Set  ([code](https://github.com/ChainsmokersAI/T5-on-ToTTo/blob/main/Evaluate.ipynb))

