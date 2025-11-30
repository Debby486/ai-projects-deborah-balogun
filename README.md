# AI Projects by Deborah Oluwatoyin Balogun

A collection of AI-powered projects, prototypes, and engineering experiments demonstrating how I build AI-native systems using LLMs, embeddings, PGVector, Celery pipelines, and real-time streaming interfaces.

These projects represent work I’ve designed and implemented in production, focusing on **semantic search**, **RAG**, **LLM-assisted workflows**, **AI automation**, and **AI-enhanced developer experiences**.

This portfolio highlights:

- OpenAI-powered embedding pipelines  
- Retrieval-Augmented Generation (RAG) using PGVector  
- LLM-driven automations for productivity  
- Multi-step agent reasoning  
- Streamed LLM responses via WebSockets  
- AI-assisted UX patterns in real applications  
- Async background processing (Celery workers)  
- Metadata-enriched reasoning flows  
- AI as a development amplifier (Cursor, ChatGPT, Claude, Copilot)  

Some implementations are internal, so this repo contains **architecture diagrams**, **pseudocode**, **sample flows**, and **redacted examples** that illustrate the engineering behind each feature.

---

# Projects Included

## **1. Help Center RAG Chatbot (PGVector + OpenAI + Streaming)**
An AI-powered support chatbot that lets users ask natural-language questions and returns answers grounded in internal Help Center documentation.

I built this end-to-end using:

- **OpenAI embeddings** for semantic search  
- **PGVector** for vector indexing and similarity search  
- **Celery background tasks** for async model processing  
- **WebSocket streaming** for real-time chatbot responses  
- A refined, user-friendly assistant response crafted with GPT  
- A controlled RAG pipeline that reduces hallucinations  

`1-help-center-chatbot-rag/`

---

## **2. AI-Powered Card Description Generator**
A feature that allows users to instantly generate rich, context-aware card descriptions using AI.

- User provides a short prompt  
- AI generates a detailed description using:  
  - user input  
  - the card’s title  
  - relevant metadata  
- Ensures consistent tone and clarity across the system  
- Uses refined prompting for UX-friendly output

`2-ai-card-description/`

---

## **3. AI Milestone Summary Generator (Sprint Retrospective Assistant)**
An AI tool that automatically summarizes all activities, cards, and subtasks in a milestone at the end of each sprint.

- Aggregates all sprint data  
- Categorizes subtasks  
- Generates a clear summary including:  
  - completed work  
  - pending work  
  - blockers  
  - key contributors  
- Greatly reduces manual reporting for team leads

`3-ai-milestone-summary/`

---

## **4. AI-Based Card Tag Generator (Semantic Tagging Engine)**
A semantic tagging system that uses AI to automatically assign relevant tags to a card based on the card’s title and content.

- Improves filtering and search  
- Groups similar issues  
- Helps surface related cards quickly  
- Uses embeddings + prompt engineering to generate consistent tags

`4-ai-card-tagging/`

---

## **5. AI Estimation Assistant (Effort & Hour Prediction)**
An AI-powered estimator that predicts effort hours for new cards by analyzing:

- Similar historic issues  
- Their previously logged hours (via the time tracker)  
- Which users completed similar work  
- The shortest completion times  
- The top 3 recommended assignees for the task  

This system uses:

- historical card embeddings  
- similarity search  
- heuristic + LLM-based reasoning  
- a clean JSON-based response format  
- controlled agent loops for stable output

`5-ai-estimation-assistant/`

---

# My AI Builder Philosophy

AI is my creative amplifier.

I use AI to:

- accelerate prototyping  
- explore ideas rapidly  
- automate complex workflows  
- generate better UX experiences  
- structure and transform data  
- scale feature development beyond normal timelines  

I experiment constantly and iterate fast, using tools like:

- ChatGPT  
- Claude  
- Cursor  
- Copilot  

to assist in code generation, prompt refinement, design reasoning, and agent behavior testing.

---


This portfolio demonstrates:

- my ability to design **AI-first systems**  
- my engineering fluency with LLMs, embeddings, and agents  
- real deployments inside production systems  
- my creativity and initiative as an AI builder  
- my commitment to learning, experimenting, and sharing

If you'd like a deeper technical walkthrough of any project, I’m happy to provide one.

