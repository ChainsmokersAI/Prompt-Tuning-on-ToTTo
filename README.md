# T5 Prompt Tuning on ToTTo Dataset (Table-To-Text Generation)
Although **T5** shows competitive performance on ToTTo dataset, it is too large to train and save the model with limited resources.<br/>
**Prompt Tuning**, a method that freezes Pre-Trained LM and prepends additional **tunable tokens** to inputs, shows comparable performance to Fine-Tuning on SuperGLUE benchmark with less memory resource.<br/>
So, I have applied Prompt Tuning (**NOT exactly same as in paper**) on ToTTo dataset (Table-To-Text Generation) and check its performance.<br/>
I have referenced the following papers:
* ToTTo: A Controlled Table-To-Text Generation Dataset ([Parikh et al.](https://arxiv.org/abs/2004.14373), 2020, [Github](https://github.com/google-research-datasets/ToTTo))
* Text-to-Text Pre-Training for Data-to-Text Tasks ([Kale and Rastogi](https://arxiv.org/abs/2005.10433), 2020)
* The Power of Scale for Parameter-Efficient Prompt Tuning ([Lester et al.](https://arxiv.org/abs/2104.08691), 2021)
## Usage (OS: Ubuntu)
### Dependencies
* jupyter
* pytorch
* sentencepiece
* (tensorboard)
### Initialize Repo
```bash
git clone https://github.com/ChainsmokersAI/Prompt-Tuning-on-ToTTo.git
cd Prompt-Tuning-on-ToTTo/
mkdir model
# Install Customized 'transformers'
pip install -e transformers/
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

# Now ALL Ready to Run Codes
```
### Run Training & Evaluation Codes (.ipynb)
Codes are in [notebook/](https://github.com/ChainsmokersAI/Prompt-Tuning-on-ToTTo/tree/main/notebook) directory and can be easily run by running cells in order (preprocessing example [codes](https://github.com/ChainsmokersAI/Prompt-Tuning-on-ToTTo/blob/main/notebook/1.%20Preprocess.ipynb) exist).<br/>
Support the following training and corresponding evaluation codes:
* Fine-Tuning ([codes](https://github.com/ChainsmokersAI/Prompt-Tuning-on-ToTTo/blob/main/notebook/2.%20Finetune.ipynb)) ([eval](https://github.com/ChainsmokersAI/Prompt-Tuning-on-ToTTo/blob/main/notebook/3.%20Evaluate.ipynb))
* Prompt Tuning-Random Init ([codes](https://github.com/ChainsmokersAI/Prompt-Tuning-on-ToTTo/blob/main/notebook/4.%20Prompt-Tuning.ipynb)) ([eval](https://github.com/ChainsmokersAI/Prompt-Tuning-on-ToTTo/blob/main/notebook/5.%20Evaluate%20(Prompt-Tuning).ipynb))
* Prompt Tuning-Sampled Vocab Init (Future Work)
### Results
All models were trained on single GPU (GeForce RTX 3090) and evaluated on dev set.<br/>
Checkpoints were saved per an epoch and the best one was chosen.
|Model|BLEU|PARENT|Size|
|----|----|----|----|
|Fine-Tuning (T5-base)<br/>batch_size 24 / lr 1e-4 / epoch 9of10|48.8|58.50|892MB|
|Fine-Tuning (T5-large)<br/>batch_size 24 / lr 1e-4 / epoch 6of10|**50.1**|**59.04**|2.95GB|
|Prompt Tuning (T5-base)<br/>prompt_len 100 / hidden_dim 768 / batch_size 8 / lr 3e-1 / epoch 18of20|42.6|55.08|*5.04MB*|
|Prompt Tuning (T5-large)<br/>prompt_len 100 / hidden_dim 768 / batch_size 8 / lr 3e-1 / epoch 16of20|44.3|56.40|*6.71MB*|

