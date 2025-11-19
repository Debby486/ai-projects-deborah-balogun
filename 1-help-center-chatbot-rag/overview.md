# Help Center RAG Chatbot (PGVector + OpenAI + Streaming)

## 1. Project Overview

This feature is an AI-powered Help Center chatbot that allows users to ask natural-language questions and get accurate answers based on existing Help Center articles.

I implemented a **Retrieval-Augmented Generation (RAG)** pipeline using:

- **OpenAI embeddings** to convert queries and documents into vectors  
- **PGVector** inside PostgreSQL to store and search embeddings  
- **Similarity search** to retrieve the most relevant Help Center articles  
- **OpenAI Chat Completions (gpt-4o-mini)** to generate a final answer  
- **Streaming responses** so users see answers appear in real time  
- A **user-friendly, support-focused tone**, refined with ChatGPT

The goal was to reduce stress for users who don’t want to click through multiple pages just to find a single answer.

## 2. High-Level Architecture

**Text version of the architecture:**

1. User opens the Help Center and asks a question in the chatbot.
2. Backend takes the user’s query and generates an **embedding** using OpenAI.
3. The query embedding is used with **PGVector** to perform a **similarity search** on Help Center article embeddings.
4. The top matching documents are combined into a **context block**.
5. The context and user query are sent to **OpenAI’s chat model (`gpt-4o-mini`)**.
6. The response is **streamed** back to the frontend via WebSockets and rendered in the chat UI.

In summary:

`User → Query → Embedding + PGVector Search → Context → OpenAI Chat Completion → Streamed Answer`


## 3. Core Retrieval + Generation Logic (Simplified)

Below is a simplified / redacted version of the core logic:

```python
# 1. Build embedding + vector store
embedding = OpenAIEmbeddings(api_key=OPENAI_API_KEY)
vectorstore = PGVector(
    connection_string=CONNECTION_STRING,
    embedding_function=embedding,
    collection_name=COLLECTION_NAME,
)

# 2. Semantic search over Help Center docs
results = vectorstore.similarity_search(query, k=3)
if not results:
    generate_assistant_message(
        "I'm sorry, I could not find any information about that."
    )
    return

# 3. Select the best link/title for the user (custom helper)
link, title = best_help_center_link(results, query)

# 4. Build retrieval context from top documents
docs_text = "\n\n".join([f"- {doc.page_content}" for doc in results])
context = f"Help Center retrieved documents:\n{docs_text}\n\n"

# 5. Stream response from the LLM
stream = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[
        {"role": "system", "content": "You are a helpful support assistant."},
        {"role": "user", "content": f"Query: {query}\n\n{context}"},
    ],
    stream=True,
)
Signal start of stream
        send_event_to_group(group, "help-center-message-start", {})

        # Send streamed chunks to frontend
        for chunk in stream:
            delta = chunk.choices[0].delta.content
            if delta:
                send_event_to_group(
                    group, "help-center-message-streamed", {"message": delta}
```
## 4. Design Decisions

- PGVector + OpenAI Embeddings  
  Using PGVector inside PostgreSQL made it easy to keep Help Center content and vectors close together, and allowed us to use SQL + vector search in the same database.

- Top-k = 3 documents  
  Limiting to the top 3 results keeps the context focused, improves answer quality, and helps stay within token limits.

- Fallback  
  When no relevant document is found, the bot responds with a friendly apology instead of returning nothing. I used ChatGPT to refine the wording so it felt empathetic and clear.

- Context formatting  
  Articles are turned into bullet points and prefixed with `"Help Center retrieved documents:"`. This made the model more likely to quote or align with the actual docs and reduced hallucinations.

- Streaming UX  
  Using streaming responses made the chatbot feel faster and more interactive. Users see answers being typed out instead of waiting for a long pause.

---

## 5. How I Used AI During Development

I didn’t only use AI to answer user queries, I also used it as a developer tool:

**Used ChatGPT to experiment with:**

- different system prompts (“You are a helpful support assistant…”)
- ways to phrase fallback messages
- ways to structure the context block to reduce hallucinations

**Used AI-assisted coding tools (e.g. ChatGPT / Cursor-like flows) to:**

- draft integration snippets  
- explore edge cases  
- brainstorm improvements to the retrieval flow  
