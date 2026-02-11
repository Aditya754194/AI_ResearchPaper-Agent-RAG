# AI Research Paper Multi-Agent System with RAG

Full-stack LangGraph workflow that validates AI topics, fetches arXiv papers, builds a Gemini-powered comprehensive summary, and enables RAG Q&A over the retrieved papers.

## Highlights
- Multi-agent pipeline (validate topic, fetch papers, summarize, build RAG, answer questions)
- Gemini for validation and comprehensive summary; Ollama for other LLM tasks
- Pinecone vector store with MiniLM embeddings for retrieval
- React + Vite frontend with a clean summary + chat experience

## API
- `POST /api/process-topic` → validate topic, fetch papers, return comprehensive summary, session ID, and readiness flags
- `POST /api/query-rag` → ask questions against the built RAG context for a session

## Setup 
1) Backend: `cd backend` then `python -m venv venv` and `venv\Scripts\activate`
2) Install backend deps: `pip install -r requirements.txt`
3) Environment: copy `.env.example` to `.env`, add `GEMINI_API_KEY`, Pinecone keys
4) Run backend: `uvicorn main:app --reload`
5) Frontend: `cd frontend` then `npm install`
6) Start frontend: `npm run dev`

## Structure
```
backend/
  main.py, graph.py, models.py, agents/, utils.py
frontend/
  src/App.jsx, src/api.js, src/components/
```
```

[Parallel Execution]
  ├─→ Comprehensive Summarizer (Agent 3)
  ├─→ Individual Paper Summarizer (Agent 4)
  └─→ RAG System Builder (Agent 5)
  ↓
END
```

## Features in Detail

### Comprehensive Summary
- **8 structured sections**: Overview, Background, Key Concepts, Technical Architecture, Applications, Research Trends, Challenges, Future Directions
- **Wikipedia-style**: Encyclopedic, informative, and complete
- **Based on 5 papers**: Synthesizes information from all retrieved papers

### Individual Paper Summaries
- **5-7 sentence summaries** covering:
  - Main research question
  - Methodology
  - Key findings
  - Significance

### RAG System
- **Vector embeddings**: Uses `all-MiniLM-L6-v2` (384 dimensions)
- **Chunking**: 500 tokens with 50-token overlap
- **Top-5 retrieval**: Most relevant chunks for each query
- **Source citations**: Shows which papers were used to answer
### 📸 Screenshots
![Topic Search Page](https://res.cloudinary.com/dccuxjsor/image/upload/v1770818358/Screenshot_2026-02-11_192159_mrbhwg.png)
![Summary and Chatbot Page](https://res.cloudinary.com/dccuxjsor/image/upload/v1770818357/Screenshot_2026-02-11_192540_h54zxp.png)
![Chatbot Answer page](https://res.cloudinary.com/dccuxjsor/image/upload/v1770818358/Screenshot_2026-02-11_192624_xqemtl.png)
  
### Author
- Aditya Kumar
- GitHub: @Aditya754194

