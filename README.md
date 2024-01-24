# ov-llm-rag

```bash
# clone the repo
git clone https://github.com/yas-sim/openvino-llm-chatbot-rag.git

# grab the docs zip
cd openvino-llm-chatbot-rag
wget https://docs.openvino.ai/archives/2023.2.zip

# extract
mkdir -p openvino_html_doc
unzip 2023.2.zip
mv 2023.2 openvino_html_doc

# install deps
pip install -r requirements.txt
python -m spacy download en_core_web_sm

# fix for latest sqlite3 in linux
pip install pysqlite3-binary
vi /home/codespace/.python/current/lib/python3.10/site-packages/chromadb/__init__.py 

# add below to top of file
__import__('pysqlite3')
import sys
sys.modules['sqlite3'] = sys.modules.pop('pysqlite3')

# export vars to current terminal
set -a; source .env; set +a

# preprocess data
python openvino-doc-specific-extractor.py
```