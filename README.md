# 📊 Financial Report Q&A — RAG Application

A Retrieval-Augmented Generation (RAG) application that lets you upload a financial report PDF (10-K, annual report, quarterly filing) and ask natural-language questions about it. Built with free, open-source tools and the Gemini API free tier.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/AkshaySarwade/financial-report-rag/blob/main/Financial_Report_RAG.ipynb)

## Why I Built This

Annual reports and 10-K filings are 100-300 pages of dense, structured information. Finding specific data points usually means manual scrolling and Ctrl+F searching.

This app makes financial documents conversational. Upload the PDF, ask questions in plain English, get grounded answers with page citations so every claim can be verified against the source.

## Try It

Click the "Open in Colab" badge above. You'll need a free Gemini API key from https://aistudio.google.com/app/apikey

Real example output, tested on Apple's FY24 Q4 financial statement:

> **Q:** What was the total revenue?
>
> **A:** For the fiscal year ended September 28, 2024, total net sales were $391,035 million. For Q4, total net sales were $94,930 million (Page 1).

## Tech Stack

- Python with pypdf for PDF extraction
- sentence-transformers/all-MiniLM-L6-v2 for embeddings
- ChromaDB as the in-memory vector store
- Google Gemini (gemini-flash-latest) as the LLM
- Google Colab as the runtime

Everything is free — no paid APIs, no GPU required, no cloud bill.

## How RAG Works Here

1. Extract text from PDF pages with pypdf
2. Chunk into ~500-word pieces with 80-word overlap
3. Embed each chunk into a 384-dim vector
4. Store in ChromaDB
5. On a question, embed the query and retrieve top-5 similar chunks
6. Pass question + chunks to Gemini with a strict instruction to use only the provided context and cite page numbers

## Honest Limitations

- Tables in PDFs are tricky — pypdf flattens table structure
- Free Gemini tier rate-limits at 15 requests/min
- Embedding model is general-purpose; finance-domain model would retrieve better
- Single-document scope only

## Author

Akshay Sarwade — [LinkedIn](https://www.linkedin.com/in/akshay0sarwade) · [GitHub](https://github.com/AkshaySarwade)
