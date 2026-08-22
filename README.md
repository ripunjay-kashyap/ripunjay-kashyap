# Ripunjay Kashyap

**AI/ML engineer, Bangalore.** I build agentic systems where the model isn't trusted with the numbers.

Rules engines own the math. LLMs own the language. Every answer cites a source, every run leaves a trace,
and every payload is honest about how much you should trust it. IEEE-published · graduated 2025 · always shipping.

[![Portfolio](https://img.shields.io/badge/ripunjay.vercel.app-black?style=flat-square&logo=vercel&logoColor=white)](https://ripunjay.vercel.app)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/ripunjay-kashyap)

---

## selected work

### [soundreverse](https://github.com/ripunjay-kashyap/soundreverse) · reverse-engineers mastering decisions from an audio fingerprint
A LangGraph multi-agent pipeline that turns a track into EQ curves, compression settings and producer notes.
The LLM writes *reason strings only* — every frequency, ratio and gain value comes from a YAML rules engine
evaluated in pure Python. A deterministic Critic runs four physical-impossibility checks and kicks the Analyst
back up to 3× until it passes. Async Supabase job queue absorbs the 70–95s pipeline without an HTTP timeout.

`LangGraph` `Groq` `FastAPI` `Modal` `React 19` `Supabase` — **[live demo](https://soundreverse.vercel.app)** · **[public LangSmith trace](https://smith.langchain.com/public/58461f05-d106-47c2-93a4-bbf8460f4c2a/r)**

### [zenic](https://github.com/ripunjay-kashyap/zenic) · advanced RAG + agent + eval, 10,201-chunk corpus
Hybrid retrieval over NIH ODS, USDA and ISSN literature: BM25 candidates injected *before* the cross-encoder
rerank so terse nutrient tables never get crowded out, per-source diversity caps, live USDA fallback when the
top rerank score drops under 0.5. BMR/TDEE math is pure Python — never delegated to the model.

**RAGAS faithfulness 0.937** · **context precision 0.911** · 33/33 unit · 12/12 router · 8/8 graph paths
`LangGraph` `ChromaDB → Qdrant` `bge-reranker` `Llama 3.3 70B` `RAGAS`

### [audio-sonic-mcp](https://github.com/ripunjay-kashyap/audio-sonic-mcp) · any song → a structured sonic signature, fully offline
Four MCP tools exposing a 6-stage pipeline: Demucs stem separation → librosa key/tempo → a 512-dim CLAP
embedding and zero-shot vibe tags. Async fire-and-forget, so heavy inference never blocks the calling agent.
Degrades to HPSS and plain feature matrices when the ML extras aren't installed.

Every payload ships a `bpm_engine` field naming the engine that produced the tempo — because the librosa
fallback can lock onto an octave multiple, and a number you can't calibrate is worse than no number.

`FastMCP` `Demucs` `LAION CLAP` `librosa` `Docker` — zero API keys, 100% local

---

## stack

[![Core](https://skillicons.dev/icons?i=python,typescript,fastapi,nextjs,react,tailwind,docker&theme=dark)](https://skillicons.dev)

| | |
|---|---|
| **agents** | LangGraph · LangChain · FastMCP · structured tool calling |
| **models** | Llama 3.3 · Gemini · Groq · HuggingFace · PyTorch · XGBoost |
| **retrieval** | Qdrant · ChromaDB · BM25 · cross-encoder rerank |
| **eval & obs** | RAGAS · LangSmith · deterministic pytest suites |
| **audio** | Demucs · LAION CLAP · librosa · FFmpeg |
| **infra** | Modal · Render · Supabase · Vercel · HF Spaces · Pydantic |
| **daily drivers** | Claude Code · Gemini CLI · antigravity |

---

> currently heads down on something new — check the repos

