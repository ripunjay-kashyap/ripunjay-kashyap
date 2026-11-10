<h1 align="center">Ripunjay Kashyap</h1>

<p align="center">
<b>AI & backend engineer · Bangalore</b><br>
I build AI systems where the LLM never produces the numbers.
</p>

<p align="center">
<a href="https://www.ripunjaykashyap.dev/"><img src="https://img.shields.io/badge/portfolio-ripunjaykashyap.dev-FF5A1F?style=flat-square&labelColor=111111" /></a>
<a href="https://www.linkedin.com/in/ripunjay-kashyap/"><img src="https://img.shields.io/badge/LinkedIn-ripunjay--kashyap-FF5A1F?style=flat-square&labelColor=111111" /></a>
<a href="https://doi.org/10.1109/ICISS63372.2025.11076255"><img src="https://img.shields.io/badge/IEEE-ICISS_2025-FF5A1F?style=flat-square&labelColor=111111" /></a>
<a href="https://www.linkedin.com/in/ripunjay-kashyap/"><img src="https://img.shields.io/badge/status-open_to_AI_%26_backend_roles-111111?style=flat-square&labelColor=FF5A1F" /></a>
</p>

---

## who does what

| | LLM | code | proof |
|:--|:--|:--|:--|
| **SoundReverse** | writes the explanation | every EQ, compression and gain value | public LangSmith trace |
| **MIMIC** | picks each persona's next action | limits actions to elements on the page | screenshot + browser event per finding |
| **Zenic** | writes the answer | retrieval, calorie math, the "I don't know" fallback | cited passages · RAGAS 0.937 |
| **Audio Sonic MCP** | none | tempo, key, stems, embeddings | `bpm_engine` on every payload |
| **SHPSv2** | none | remaining-useful-life estimates | SHAP attribution per estimate |

---

## builds

### SoundReverse
**Estimates the EQ, compression and gain settings used to master a track.**

![](https://img.shields.io/badge/stems-4-FF5A1F?style=flat-square&labelColor=111111)
![](https://img.shields.io/badge/critic_checks-4-FF5A1F?style=flat-square&labelColor=111111)
![](https://img.shields.io/badge/max_retries-3-FF5A1F?style=flat-square&labelColor=111111)
![](https://img.shields.io/badge/run_time-70–95s-FF5A1F?style=flat-square&labelColor=111111)
&nbsp;·&nbsp; [code](https://github.com/ripunjay-kashyap/soundreverse) · [live demo](https://soundreverse.vercel.app/) · [trace](https://smith.langchain.com/public/58461f05-d106-47c2-93a4-bbf8460f4c2a/r)

<details>
<summary><b>how it works</b></summary>
<br>

```
track ─▶ demucs (4 stems) ─▶ analyst ─▶ critic ─┬─▶ EQ curves, compression, producer notes
                                ▲               │
                                └── fails check ┘  (up to 3x)
```

A LangGraph multi-agent pipeline. The LLM writes only the reasoning. Every frequency, ratio and gain comes from a YAML rules engine evaluated in Python. The critic is deterministic: four physical-impossibility checks, and the analyst goes back until it passes. A run takes 70 to 95 seconds, so jobs live on an async Supabase queue rather than inside an HTTP request.

`LangGraph` `Groq` `FastAPI` `Modal` `React 19` `Supabase`
</details>

### MIMIC
**Six AI personas test a website in parallel and report where they got stuck, with screenshots.**

![](https://img.shields.io/badge/personas-6-FF5A1F?style=flat-square&labelColor=111111)
![](https://img.shields.io/badge/runs-parallel-FF5A1F?style=flat-square&labelColor=111111)
![](https://img.shields.io/badge/every_finding-screenshot_%2B_event-FF5A1F?style=flat-square&labelColor=111111)
&nbsp;·&nbsp; [code](https://github.com/ripunjay-kashyap/MIMIC) · [live demo](https://mimic-teal-one.vercel.app/)

<details>
<summary><b>how it works</b></summary>
<br>

Each persona walks the same flow (home → details → OTP → confirmed) in its own browser. Personas can only interact with elements that really exist on the page, and each reported issue links to its screenshot and browser event.

`LangGraph` `Playwright` `FastAPI`
</details>

### Audio Sonic MCP
**An MCP server that pulls tempo, key, stems and a CLAP embedding from any song. Runs offline.**

![](https://img.shields.io/badge/MCP_tools-4-FF5A1F?style=flat-square&labelColor=111111)
![](https://img.shields.io/badge/pipeline_stages-6-FF5A1F?style=flat-square&labelColor=111111)
![](https://img.shields.io/badge/CLAP_embedding-512d-FF5A1F?style=flat-square&labelColor=111111)
![](https://img.shields.io/badge/API_keys-0-FF5A1F?style=flat-square&labelColor=111111)
&nbsp;·&nbsp; [code](https://github.com/ripunjay-kashyap/audio-sonic-mcp) · [LobeHub](https://lobehub.com/mcp/ripunjay-kashyap-audio-sonic-mcp) · I maintain it

<details>
<summary><b>how it works</b></summary>
<br>

Demucs stem separation → librosa key and tempo → a LAION CLAP embedding → zero-shot vibe tags. The MCP server and the CLI share one engine. Calls are fire-and-forget, so long inference jobs don't block the calling agent. Without the ML extras installed, it falls back to HPSS and plain feature matrices instead of crashing.

`FastMCP` `PyTorch` `Demucs` `LAION CLAP` `librosa` `Docker`
</details>

### Zenic
**A nutrition and exercise assistant that cites its sources and says when it doesn't know.**

![](https://img.shields.io/badge/corpus-10,201_chunks-FF5A1F?style=flat-square&labelColor=111111)
![](https://img.shields.io/badge/faithfulness-0.937-FF5A1F?style=flat-square&labelColor=111111)
![](https://img.shields.io/badge/context_precision-0.911-FF5A1F?style=flat-square&labelColor=111111)
![](https://img.shields.io/badge/tests-53%2F53-FF5A1F?style=flat-square&labelColor=111111)
&nbsp;·&nbsp; [code](https://github.com/ripunjay-kashyap/zenic) · [demo video](https://youtu.be/H_UBmU1cgM8)

<details>
<summary><b>how it works</b></summary>
<br>

Hybrid retrieval over NIH ODS, USDA and ISSN literature. BM25 candidates are added before the cross-encoder rerank, per-source caps keep any one source from dominating, and when the best rerank score falls under 0.5 it pulls live USDA data instead. BMR and TDEE are computed in Python. Tests: 33 unit, 12 router, 8 graph paths.

`LangGraph` `Starlette` `ChromaDB → Qdrant` `bge-reranker` `Llama 3.3 70B` `RAGAS`
</details>

### SHPSv2
**Predicts remaining useful life for bridges from sensor data, with SHAP explanations.**

![](https://img.shields.io/badge/output-remaining_useful_life-FF5A1F?style=flat-square&labelColor=111111)
![](https://img.shields.io/badge/explained_by-SHAP-FF5A1F?style=flat-square&labelColor=111111)
&nbsp;·&nbsp; [code](https://github.com/ripunjay-kashyap/shps-v2) · [live demo](https://huggingface.co/spaces/Ripunk/shps-v2)

<details>
<summary><b>how it works</b></summary>
<br>

Sensor readings plus physics-based features feed an XGBoost / Keras model. Every estimate comes with a SHAP breakdown of which readings pushed it up or down.

`XGBoost` `Keras` `SHAP`
</details>

---

## problems I hit

| problem | fix |
|:--|:--|
| the cross-encoder ranked short nutrient tables below longer text chunks | inject BM25 candidates before reranking |
| librosa can report double or half the real tempo | every tempo includes the engine that measured it |
| a 70–95 s pipeline run exceeds HTTP timeouts | async job queue on Supabase |
| an LLM reviewing another LLM's output | a rule-based critic with four physics checks |

---

## stack

| | |
|:--|:--|
| **agents & retrieval** | LangGraph · LangChain · FastMCP · Qdrant · ChromaDB · BM25 · cross-encoder rerank |
| **models** | PyTorch · TensorFlow / Keras · XGBoost · scikit-learn · SHAP · Llama 3.3 · Gemini · Groq |
| **audio & speech** | HTDemucs · LAION CLAP · librosa · WhisperX · Kokoro / Qwen TTS · FFmpeg |
| **backend & ops** | FastAPI · Flask · Starlette · Pydantic v2 · PostgreSQL · Supabase · Docker · Modal |
| **eval** | RAGAS · LangSmith · pytest |
| **front end** | React · Next.js · Tailwind · Vite · Flutter · Mapbox GL JS |

---

## also

- **IEEE ICISS 2025**: [AR/VR based Campus Navigation System](https://doi.org/10.1109/ICISS63372.2025.11076255). Lead researcher and developer. Flutter + Mapbox + ARCore + Unity, using a GPS dataset we collected by walking the campus.
- **B.E. Computer Science**, Sathyabama Institute of Science and Technology, 2021–2025.

<p align="center"><sub>working on something new.</sub></p>
