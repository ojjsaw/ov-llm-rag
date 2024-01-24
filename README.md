# ov-llm-rag

```bash
# clone the repo
git clone https://github.com/yas-sim/openvino-llm-chatbot-rag.git

# grab the docs zip
wget https://docs.openvino.ai/archives/2023.2.zip

# extract
cd openvino-llm-chatbot-rag
mkdir -p openvino_html_doc
unzip 2023.2.zip -d openvino_html_doc

# install deps
pip install -r requirements.txt
python -m spacy download en_core_web_sm

# export vars to current terminal
set -a; source .env; set +a

# preprocess data
python openvino-doc-specific-extractor.py
```