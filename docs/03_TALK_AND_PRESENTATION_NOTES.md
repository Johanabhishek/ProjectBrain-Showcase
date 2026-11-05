# ProjectBrain — Talk & Presentation Notes

> Use this outline for technical talks, investor/engineering demos, and architecture reviews.

---

## Slide 1: The Core Problem with AI Coding Agents Today
- **How AI agents debug today:** They play 20 Questions with your codebase—running `grep`, reading 1,500-line files into context, running a test, reading a stack trace, re-reading the same file, and compacting their context window when it overflows.
- **Why RAG & Symbol Maps fail on real bugs:**
  - **Vector Embeddings (Cursor/Windsurf):** Know *text similarity*, not *execution flow* or *database constraints*.
  - **1-Layer Symbol Maps (Aider RepoMap / LSP):** Stop at language boundaries. They cannot connect a React `fetch()` call to a FastAPI `@router.post` handler, a SQL `CREATE TABLE` migration, and a background worker.

---

## Slide 2: What Makes ProjectBrain a Monster (5 Simple Lines)
1. **One Connected Circuit Across Languages:** Links React JS $\xrightarrow{\text{http\_flow}}$ FastAPI Python $\xrightarrow{\text{calls}}$ Auth Helpers $\xrightarrow{\text{state\_flow}}$ SQL Tables & Workers in one unified graph.
2. **Finds Bugs *Before* Running Code:** Mathematically verifies SQL `NOT NULL` schemas, SQLite/Postgres dialects, `UUID` vs. `TEXT` types, `SELECT` column projections, and HTTP verb/response shapes in `<1s`.
3. **Symptom-to-Guard Causal Chop:** Give it an error code (`403`), and it intersects the forward call cone from the frontend with the backward origin cone of `403` to hand you the exact `if` statement in `deps.py`.
4. **Zero-Waste Working Memory:** Tracks an Interval Tree of every line the LLM has already seen—never emitting duplicate lines in the same session.
5. **Pre-Disk Self-Verifying Patch Engine:** Tests every code edit *in memory* for both AST syntax and 7-way cross-boundary contracts before touching the hard drive.

---

## Slide 3: The Math Under the Hood
- **6D Behavioral Coordinate Matrix:**
  $$\mathcal{C}(b) = \bigl(X_{\text{scope}},\; Y_{\text{role}},\; \Delta Z_{\text{write}},\; Z_{\text{read}},\; W_{\text{calls}},\; E_{\text{exit}},\; T_{\text{mode}}\bigr)$$
- **Multiplex Personalized PageRank:**
  $$\vec{\pi}^{(t+1)} = (1 - \alpha)\,\mathbf{P}_{\text{multiplex}}^{\top}\,\vec{\pi}^{(t)} + \alpha\,\vec{v}_0$$
- **Causal Program Chop:**
  $$\mathcal{X}_{\text{chop}}(S_0, \Sigma) = \mathcal{F}_{\text{multiplex}}^{\le 4}(S_0) \;\cap\; \mathcal{B}(\Sigma)$$
- **Submodular Marginal Gain per Unseen Token:**
  $$u^* = \arg\max_{u} \frac{\pi_{\text{PPR}}(u) \cdot \Delta \mathcal{I}(u \mid \mathcal{U}_{\text{cov}})}{C_{\text{unseen}}(u)^{0.55}}$$

---

## Slide 4: Live Demo Flow (1-Command Root-Cause Proof)
1. **Prompt:** `"uploadBatchFile fails with 403 or database constraint error and worker job processing"`
2. **Command:** `projectbrain dossier "..."`
3. **Output (<1s, 0 tests executed):**
   - Traces `frontend/src/api/client.js:uploadBatchFile` $\to$ `backend/app/routers/uploads.py:upload_file` $\to$ `backend/app/deps.py:load_batch` (`L19: raise ApiError(403, "forbidden")`).
   - Pinpoints `uploads.py:L87`, `L121`, `L141`, `L287` missing `NOT NULL` columns (`created_at`, `run_after`) against `local_db.py` and `.sql` migrations.
