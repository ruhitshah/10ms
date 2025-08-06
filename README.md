Bengali RAG (Retrieval-Augmented Generation) System
This repository implements a Retrieval-Augmented Generation (RAG) system to answer questions based on a Bengali document (PDF) using the LangChain framework, Groq LLM (Large Language Model), and FAISS vector store. It preprocesses the PDF, splits the text into chunks, creates a vector store, and uses Groq's LLM to answer queries related to Bengali literature.

Features:
Extracts text from a Bengali PDF using the bangla_pdf_ocr library.

Preprocesses the text, cleans it, and splits it into chunks.

Uses HuggingFace embeddings for Bengali to generate embeddings for the document's text.

Stores the embeddings in a FAISS vector store for fast retrieval.

Uses Groq’s LLM to answer the queries based on the context retrieved from the vector store.

The system supports a RetrievalQA chain to answer queries based on relevant context extracted from the document.

Setup
Prerequisites
Python 3.6 or higher

Install necessary Python packages:

pip install langchain langchain_groq langchain_huggingface langchain_community faiss-cpu tenacity bangla_pdf_ocr numpy python-dotenv
Note: Make sure to replace the GROQ_API_KEY in the script with your actual API key for Groq.

Environment Setup
Clone this repository or download the script.

Set up your environment variables (for example, GROQ_API_KEY should be set in your environment).

Make sure you have access to a Groq API key, and use it directly in the script.

Script Overview
1. Text Extraction from PDF:
The script uses bangla_pdf_ocr to extract text from the PDF (HSC26-Bangla1st-Paper.pdf), saving it to a .txt file to avoid re-processing the PDF each time.

The text is cleaned and split into manageable chunks.

2. Vector Store Creation:
The script utilizes HuggingFace’s Bengali sentence similarity model to create embeddings for the extracted text.

The embeddings are stored in a FAISS vector store to enable fast similarity-based retrieval.

3. Groq LLM Initialization:
The script initializes the Groq LLM (Large Language Model) and uses it to answer queries based on the retrieved context from the document.

4. Query Evaluation:
It evaluates multiple queries with expected answers and compares the actual responses from the model with the expected ones using cosine similarity.

5. Expected Output:
For each query, the system compares the answer with the expected one and calculates the cosine similarity between the expected and actual answers.

Running the Script
To run the script, use the following command:

python rag_system.py
Make sure you have the correct paths for the PDF_PATH and TEXT_PATH variables.

Example Output:
Here’s an example of the output you can expect when running the system:

Query: অনুপমের ভাষায় সুপুরুষ কাকে বলা হয়েছে?
Expected: শুম্ভুনাথ
Actual: শুম্ভুনাথকে বলা হয়েছে

Query: কাকে অনুপমের ভাগ্য দেবতা বলে উল্লেখ করা হয়েছে?
Expected: মামাকে
Actual: মামাকে অনুপমের ভাগ্য দেবতা বলে উল্লেখ করা হয়েছে

Query: বিয়ের সময় কল্যাণীর প্রকৃত বয়স কত ছিল?
Expected: ১৫ বছর
Actual: ১৪ বছর
Query: The question that is being asked.

Expected: The expected correct answer for comparison.

Actual: The answer returned by the Groq LLM based on the context retrieved from the document.

Cosine Similarity: A numerical value representing how similar the actual answer is to the expected answer.
