# AlphaStorm🌪️: NLP with FAISS & BM25
## Introduction

<p align="center">
  <img src="image.png" width="400">
</p>

This chatbot recommends popular restaurants in Jeju Island based on data provided by Shinhan Card. 🏝️🍽️🍊

By classifying locations into hot places 🔥 and cool places ❄️, it suggests well-known and hidden gems depending on the user’s query and context.

The service is implemented using the RAG (Retrieval-Augmented Generation) technique and LLM (Large Language Models) to enhance recommendation accuracy. 🤖

🎉 ⭐ This project was recognized for its innovation and received an award in the 2024 Bigcontest Generative-AI Session ⭐ 🎉

## Setup

### 1. Environment Configuration
Ensure you have Python 3.8 or later installed.

Install the required dependencies:

```bash
pip install -r requirements.txt
```



### 2. Prepare Data
The dataset is private and provided by the contest organizers. It is not included in this repository.

Place the dataset in the `./data` directory before running the code.



### 3. Run the Code
(1) Generate and Store Embeddings
Run the following command to generate embeddings and save the FAISS index:
```bash
python embeddings.py
```

(2) Data Processing
You can preprocess the data using chunking.py or sentences.py:
```bash
python chunking.py
python sentences.py
```

(3) Run the Web Application
To launch the Streamlit-based web application, execute:
```bash
streamlit run alphastorm_app.py
```

## Data Notice
This project uses private data provided by contest organizers. The dataset is not included in this repository. 

Users must prepare and place the data manually.
