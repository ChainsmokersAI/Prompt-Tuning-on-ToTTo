# T5 on Table-To-Text Generation: ToTTo

## Usage
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

# Evaluation Codes DO NOT Work on Recent Version of 'sacrebleu'
pip uninstall sacrebleu
pip install sacrebleu==1.5.1
```

