# RAG-Powered Review Search: "Ask Your Reviews"

## Business Question
Can a system answer specific questions about customer feedback by retrieving only the most relevant reviews and generating a grounded answer — rather than requiring someone to manually read through every review, or relying on an AI's generic guess?

## Dataset
Women's E-Commerce Clothing Reviews (Kaggle) — licensed CC0: Public Domain, free to use and share with no restrictions.

## Tools Used
Python, Google Gemini API (`gemini-embedding-001` for embeddings, `gemini-3.5-flash-lite` for generation), pandas, numpy

## What This Demonstrates
This project implements Retrieval-Augmented Generation (RAG) from scratch, without a pre-packaged framework, to show genuine understanding of the mechanics rather than just calling a library:
1. **Embedding** — converting review text into numerical vectors that capture meaning
2. **Retrieval** — measuring cosine similarity between a question's embedding and every review's embedding to find the most relevant matches
3. **Augmented Generation** — passing only the retrieved, relevant reviews to an LLM as context, so its answer is grounded in real data rather than general knowledge

## Approach
1. Loaded a sample of real customer reviews
2. Generated an embedding for each review using Gemini's embedding model
3. Built a cosine similarity function to measure how closely two embeddings match in meaning
4. Took a natural-language question, embedded it the same way, and ranked all reviews by similarity to find the most relevant ones
5. Passed the top-ranked reviews to an LLM alongside the original question, instructing it to answer using only that retrieved context

## Example Result
**Question asked:** "What do customers complain about with sizing?"

The system correctly retrieved reviews about restricted movement, items running small, and specific sizing details (e.g. a customer going from a 6/28 to a medium) — then generated an answer citing these specific, real details rather than a generic response about sizing in general.

## Scope Note
This implementation stores embeddings in memory (a Python list) rather than a dedicated vector database (like Pinecone, Chroma, or FAISS), since the dataset here is small. The underlying retrieval logic — embedding, cosine similarity, ranking — is identical to what a production vector database does at scale; a real vector database simply makes this search fast and efficient across millions of documents instead of a few dozen.

## Files
- `rag_review_search.ipynb` — full notebook with code, retrieval logic, and example results
- `Womens Clothing E-Commerce Reviews.csv` — dataset used for this analysis (CC0 licensed)
