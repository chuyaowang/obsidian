# Gemini File Search API

#agent 
[Documentation Link](https://ai.google.dev/gemini-api/docs/file-search)

**File Search** is a powerful tool in the Gemini API that enables **Retrieval Augmented Generation (RAG)**. Instead of relying solely on the model's pre-trained knowledge or stuffing a massive prompt with text, File Search allows you to upload documents, index them, and let the model "search" through them to find relevant answers to user queries.

This guide covers how it works, how to implement it, and best practices.

---

## 1. How File Search Works

At its core, File Search bridges your proprietary data with the Gemini model. Here is the lifecycle of a File Search request:

1. **Ingestion (Upload & Index):** You upload documents (PDFs, text files, code, etc.) to a **File Search Store**.
2. **Processing:** Google automatically:
* **Chunks** your documents into smaller pieces.
* **Embeds** them (converts text to vector numbers representing meaning).
* **Indexes** them for fast retrieval.


3. **Retrieval (The "Search"):** When a user asks a question, the system performs a **semantic search** across your File Search Store to find the most relevant chunks.
4. **Generation:** The relevant chunks are retrieved and fed into the Gemini model as context. The model then answers the user's question using *your* data as the source of truth.

**Key Benefit:** You only pay for the indexing (one-time) and the generation. **Storage and query-time retrieval are free.**

---

## 2. Step-by-Step Implementation Guide

To use File Search, you typically use the Python or Node.js SDK. Below is the Python workflow.

### Step 1: Setup

Ensure you have the latest library:

```bash
pip install -U google-genai

```

### Step 2: Create a File Search Store

Think of a "Store" as a folder or a database collection for a specific topic (e.g., "Financial Reports 2024").

```python
from google import genai

client = genai.Client(api_key="YOUR_API_KEY")

# Create a store
file_search_store = client.file_search_stores.create(
    config={'display_name': 'my_knowledge_base'}
)
print(f"Store created: {file_search_store.name}")

```

### Step 3: Upload Files to the Store

You can upload files directly to the store. The API handles the parsing and indexing automatically.

```python
# Upload a file directly to the store
operation = client.file_search_stores.upload_to_file_search_store(
    file='company_policy.pdf',
    file_search_store_name=file_search_store.name,
    config={
        'display_name': 'Company Policy 2025'
    }
)

# Wait for the file to be processed (indexing takes a moment)
import time
while not operation.done:
    time.sleep(2)
    operation = client.operations.get(operation)

print("File processed successfully.")

```

### Step 4: Query the Model with File Search

Now, you simply tell the model to use this "tool" when answering.

```python
from google.genai import types

response = client.models.generate_content(
    model="gemini-1.5-flash", # or gemini-1.5-pro
    contents="What is the policy on remote work?",
    config=types.GenerateContentConfig(
        tools=[
            types.Tool(
                file_search=types.FileSearch(
                    file_search_store_names=[file_search_store.name]
                )
            )
        ]
    )
)

print(response.text)

```

---

## 3. Advanced Features

### Metadata Filtering

If you dump thousands of files into a store, you might want to restrict a search to specific documents (e.g., only "2023" files). You can tag files with metadata during upload and filter during generation.

**Add Metadata:**

```python
client.file_search_stores.upload_to_file_search_store(
    file='report_2023.pdf',
    file_search_store_name=file_search_store.name,
    config={
        'custom_metadata': [{'key': 'year', 'numeric_value': 2023}]
    }
)

```

**Filter Query:**

```python
# Inside your tool configuration
file_search=types.FileSearch(
    file_search_store_names=[file_search_store.name],
    metadata_filter="year = 2023" # Only search files tagged with year 2023
)

```

### Citations

For trust and verification, Gemini provides **citations** indicating exactly which file and which segment was used to generate the answer.

```python
# Accessing citations in the response
print(response.candidates[0].grounding_metadata)

```

### Custom Chunking

By default, Google handles chunking. However, you can control the chunk size if your data requires it (e.g., keeping larger sections of code together).

* **Max tokens per chunk** (e.g., 200)
* **Max overlap tokens** (e.g., 20)

---

## 4. Important Details

* **Supported Models:**
	* [`gemini-3-pro-preview`](https://ai.google.dev/gemini-api/docs/models#gemini-3-pro)
	- [`gemini-2.5-pro`](https://ai.google.dev/gemini-api/docs/models#gemini-2.5-pro)
	- [`gemini-2.5-flash`](https://ai.google.dev/gemini-api/docs/models#gemini-2.5-flash) and its preview versions
	- [`gemini-2.5-flash-lite`](https://ai.google.dev/gemini-api/docs/models#gemini-2.5-flash-lite) and its preview versions
* **Supported File Types:** Highly versatile. Supports text (`.txt`, `.md`, `.csv`), documents (`.pdf`, `.docx`, `.pptx`), and code (`.py`, `.js`, `.html`).
* **Data Persistence:**
	* **File Search Stores:** Data lives here indefinitely until you delete it.
	* **Raw Uploads:** If you upload a file via the standard Files API (not directly to a store), it is deleted after 48 hours. Always use a Store for persistent apps.

* **Limits:**
* Max 100 Stores per project.
* Standard limits on file size (2GB per file).

### Summary Table

| Feature | Description |
| --- | --- |
| **Store** | The container for your indexed files. |
| **Tool** | The mechanism (`types.Tool`) to connect a Store to the Model. |
| **Filtering** | Using key-value metadata to narrow down search scope. |
| **Cost** | **Indexing:** Paid. **Storage:** Free. **Query:** Free (you only pay for input/output tokens). |
