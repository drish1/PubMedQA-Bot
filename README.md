# Q-Abot: Biomedical Question Answering System using RAG

A lightweight Retrieval-Augmented Generation (RAG) chatbot for answering biomedical questions using scientific literature from the PubMedQA dataset. The system combines semantic search with a Large Language Model (LLM) to generate context-aware answers grounded in biomedical research.

## Overview

Q-Abot retrieves relevant biomedical abstracts from the PubMedQA dataset using vector similarity search and then uses a language model to generate answers based on the retrieved scientific context.

### Workflow

1. Load and preprocess biomedical research abstracts from PubMedQA.
2. Generate dense vector embeddings using Sentence Transformers.
3. Store embeddings in a FAISS vector index.
4. Retrieve the most relevant contexts for a user query.
5. Augment the query with retrieved scientific evidence.
6. Generate an answer using TinyLlama.

## Architecture

```text
User Question
      │
      ▼
Sentence Transformer
(Query Embedding)
      │
      ▼
FAISS Vector Search
      │
      ▼
Top-k Relevant PubMed Contexts
      │
      ▼
Prompt Construction
      │
      ▼
TinyLlama LLM
      │
      ▼
Generated Biomedical Answer
```

## Dataset

This project uses the PubMedQA dataset:

- Dataset: PubMedQA
- Source: QiaoJin/PubMedQA (Hugging Face)
- Subset: `pqa_labeled`

PubMedQA contains biomedical research abstracts paired with expert-curated questions and answers.

## Technologies Used

- Python
- Hugging Face Datasets
- Sentence Transformers
- FAISS
- Transformers
- TinyLlama-1.1B-Chat
- PyTorch
- NumPy
- Pandas

## Installation

Clone the repository:

```bash
git clone https://github.com/your-username/q-abot.git
cd q-abot
```

Install dependencies:

```bash
pip install datasets transformers sentence-transformers faiss-cpu accelerate torch pandas numpy
```

## Model Components

### Embedding Model

```python
sentence-transformers/all-MiniLM-L6-v2
```

Used to convert biomedical abstracts and user queries into dense vector representations for semantic search.

### Retrieval Engine

```python
FAISS IndexFlatL2
```

Performs efficient nearest-neighbor search over embedded biomedical documents.

### Language Model

```python
TinyLlama/TinyLlama-1.1B-Chat-v1.0
```

Generates answers using the retrieved biomedical contexts.

## Usage

Run the notebook and ask biomedical questions:

```python
question = "Is standard chemotherapy superior to molecularly targeted therapy in treating advanced NSCLC patients?"

response = ask_pubmed_bot(question)

print(response)
```

### Example Query

**Input**

```text
Is standard chemotherapy superior to molecularly targeted therapy in treating advanced NSCLC patients?
```

**Process**

1. Retrieve the most relevant PubMed abstracts.
2. Construct a context-aware prompt.
3. Generate an answer using TinyLlama.

**Output**

```text
Answer generated based on retrieved biomedical evidence.
```

## Retrieval-Augmented Generation (RAG)

The project follows the RAG paradigm:

- **Retrieval:** Fetches relevant scientific literature from PubMedQA.
- **Augmentation:** Injects retrieved context into the prompt.
- **Generation:** Produces evidence-grounded answers using an LLM.

This approach helps reduce hallucinations and improves factual accuracy compared to standalone language models.

## Project Structure

```text
q-abot/
│
├── q-abot.ipynb          # Main notebook
├── README.md            # Project documentation
└── requirements.txt     # Dependencies
```

## Future Improvements

- Support larger biomedical datasets.
- Replace TinyLlama with domain-specific biomedical LLMs.
- Implement hybrid retrieval (BM25 + Dense Retrieval).
- Add evaluation metrics (Exact Match, F1 Score).
- Deploy as a web application using Streamlit or Gradio.
- Integrate citation generation for retrieved research papers.

## Limitations

- Uses a relatively small subset of PubMedQA for demonstration.
- TinyLlama is not specifically trained for biomedical reasoning.
- Retrieval quality depends on embedding model performance.
- Answers are constrained by retrieved context coverage.

## Results

The system demonstrates how RAG can be applied to biomedical question answering by combining:

- Semantic retrieval with Sentence Transformers
- Efficient vector search using FAISS
- Context-aware response generation using TinyLlama

This creates a lightweight and scalable biomedical QA pipeline suitable for research and educational purposes.

## License

This project is intended for educational and research purposes.

## Acknowledgements

- Hugging Face Datasets
- Sentence Transformers
- FAISS
- TinyLlama
- PubMedQA Dataset

---
**Author:** Drishti
**Project:** Q-Abot – Biomedical Retrieval-Augmented Question Answering System
