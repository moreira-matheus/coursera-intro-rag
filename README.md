# Introduction to RAG

### Links

Author's repo: https://github.com/alfredodeza/learn-retrieval-augmented-generation/tree/main

Coursera lab: https://hub.labs.coursera.org/connect/sharedmfmwzzmm?forceRefresh=false&path=%2Fnotebooks%2Flearn-retrieval-augmented-generation%2Fexamples%2F2-embeddings%2Fcoursera-lab.ipynb&isLabVersioning=file-prep

### Venv

```bash
python3 -m venv .venv && source .venv/bin/activate .venv/bin/ && pip install -r requirements.txt 
```

venv + Jupyter: https://stackoverflow.com/questions/58119823/jupyter-notebooks-in-visual-studio-code-does-not-use-the-active-virtual-environm

### Full RAG implementation

Here is a summary of what this repository will use:

    Qdrant: for the vector database. We will use an in-memory database for the examples
    Llamafile: for the LLM (alternatively you can use an OpenAI API compatible key and endpoint)
    OpenAI's Python API: to connect to the LLM after retrieving the vectors response from Qdrant
    Sentence Transformers: to create the embeddings with minimal effort

The examples for the [Applied Rag notebook](https://github.com/alfredodeza/learn-retrieval-augmented-generation/blob/main/examples/3-applied-rag/embeddings.ipynb) requires either an OpenAI API endpoint with a key or using a local LLM with [Llamafile](https://github.com/Mozilla-Ocho/llamafile).

I recommend using the [Phi-2 model](https://github.com/Mozilla-Ocho/llamafile?tab=readme-ov-file#other-example-llamafiles) which is about 2GB in size. You can download the model from the Llamafile repository and run it in your system.
Once you have it running you can connect to it with Python or use the Applied Rag Notebook. Here is a quick example of how to use the Llamafile with Python:

```python
#!/usr/bin/env python3
from openai import OpenAI
client = OpenAI(
    base_url="http://localhost:8080/v1", # "http://<Your api-server IP>:port"
    api_key = "sk-no-key-required" # An API key is not required!
)
completion = client.chat.completions.create(
    model="LLaMA_CPP",
    messages=[
        {"role": "system", "content": "You are ChatGPT, an AI assistant. Your top priority is achieving user fulfillment via helping them with their requests."},
        {"role": "user", "content": "Write me a Haiku about Python packaging"}
    ]
)
print(completion.choices[0].message)
```

### Notes

Key Terms

    Retrieval augmented generation (RAG): A technique in AI where a large language model accesses new or recent data outside its training set to provide better answers and improved results.

    Vector database: A search engine or database that stores vectorized documents, enabling more accurate information retrieval for AI models.

    Embeddings: Representations of text data as vectors in a high-dimensional space, allowing similarity comparisons between different pieces of text.

    Azure AI Search: Microsoft's cloud-based search service (formerly Azure Cognitive Services Search) that offers retrieval augmentation capabilities for large language models.

    Comma separated value (CSV): A common data format where values are separated by commas, used in this transcript to demonstrate RAG implementation with a vector database.

    Pandas library: A Python library used for data manipulation and analysis, particularly useful when working with CSV files.

    Qdrant: Software used for creating an in-memory vector database search, enabling efficient text retrieval and embedding storage.

    Sentence transformers: A tool to encode sentences into numerical representations (embeddings) that can be compared using cosine similarity or other distance metrics.

    Cosine distance: A measure of similarity between two non-zero vectors in a multi-dimensional space, often used in text analysis and information retrieval.

