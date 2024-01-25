# ov-llm-rag

```bash
# clone the repo
git clone https://github.com/yas-sim/openvino-llm-chatbot-rag.git

# grab the docs zip
cd openvino-llm-chatbot-rag
wget https://docs.openvino.ai/archives/2023.2.zip

# extract
mkdir -p openvino-html-doc
unzip 2023.2.zip
mv 2023.2 openvino-html-doc

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

```bash
pip install b2

keyID:
0045442a96cfe890000000001

keyName:
ov-llm-rag

applicationKey:
K004eMCsNCCB+J9lJijNX1XyesdLZro

cd openvino-llm-chatbot-rag
b2 sync .vectorstore_300_0 b2://ov-llm-rag/.vectorstore_300_0

b2 sync openvino-html-doc b2://ov-llm-rag/openvino-html-doc
b2 upload-file ov-llm-rag limited-vectorstore_300_0.zip limited-vectorstore_300_0.zip



```

Reduce file count to test:
```bash
# check num of html files
find openvino-html-doc -type f -name "*.html" | wc -l
orig: 5051

# after removing /api* dir
non /api: 2658

# handpick remove certain deep api html files
find openvino-html-doc -type f -name "*structov*.html" -exec rm {} \;
find openvino-html-doc -type f -name "*namespacegraph*.html" -exec rm {} \;
find openvino-html-doc -type f -name "*enumov*.html" -exec rm {} \;
find openvino-html-doc -type f -name "*classov*.html" -exec rm {} \;
find openvino-html-doc -type f -name "*classngraph*.html" -exec rm {} \;
find openvino-html-doc -type f -name "*classopenvino*.html" -exec rm {} \;
find openvino-html-doc -type f -name "*enumInferenceEngine*.html" -exec rm {} \;
find openvino-html-doc -type f -name "*enumngraph*.html" -exec rm {} \;
find openvino-html-doc -type f -name "*openvino_docs_ops*.html" -exec rm {} \;
find openvino-html-doc -type f -name "*namespaceov*.html" -exec rm {} \;
find openvino-html-doc -type f -name "*namespacengraph*.html" -exec rm {} \;

after deep certain-api-html-files: 1092

# find openvino-html-doc -type f -name "*classInferenceEngine*.html" -exec rm {} \;
# find openvino-html-doc -type f -name "*openvino_docs_OV_UG_lpt*.html" -exec rm {} \;

# run once downloading of models
python llm-model-downloader.py

```