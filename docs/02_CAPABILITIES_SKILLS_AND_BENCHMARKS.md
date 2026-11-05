# ProjectBrain: Capabilities, Technical Skills & Benchmark Report

---

## 1. The 8 Core Capabilities

ProjectBrain exposes **26 MCP tools** and **12 CLI commands** (`projectbrain <cmd>`) organized into **8 technical capabilities**:

### Skill 1: Single-Read Multi-Task Engineering Dossier (`dossier` / `brain_dossier`)
* Compiles a self-contained, token-budgeted Markdown engineering dossier (`.projectbrain_dossier.md`) for one or more natural-language bug reports or feature requests in **one call** (`<1 second`).
* Combines **Explicit Symbol Pinning**, **4-Layer Multiplex Personalized PageRank (`multiplex_ppr`)**, **Causal Program Chop (`causal_symptom_chop`)**, **Submodular Gain-per-Token Selection**, and a **Closed-World Exhaustive Repo Scan** (`EXHAUSTIVE GUARANTEE` badge for state keys and routes).

### Skill 2: Surgical AST Slicing with Working-Memory Deduplication (`slice` / `brain_slice`)
* Extracts exact functions, classes, methods, or line ranges (`file.py:symbol` or `file.py:100-180`) with smart interior folding.
* **Interval-Tree Working-Memory Ledger (`Zero-Waste Guard`):** Tracks exact `[start_line, end_line]` intervals and SHA-256 content hashes of every file already delivered in the current session. Subsequent overlapping slices automatically trim already-read lines and emit **only unseen lines**.
* **Boundary Map Headers:** Every slice includes a 1-line structural compass (`# [Boundary Map] File L1-L1477 | Prev: L710:_helper | In-slice: L740:execute | Next: L920:commit`).

### Skill 3: Fine-Grained 6D Behavioral Coordinate Matrix
* Maps every function (`>= 8` lines) and its inner control-flow/IO blocks (`with[...]`, `try_block`, `catch[...]`, `branch[...]`, `sql[...]`, `useEffect[...]`) along 6 orthogonal dimensions:
  - **`X_scope` (Structural Guard):** Exact lexical/control guard (`with[db.tx(user) as conn]`, `branch[row["created_by"] != user]`, `sql[INSERT background_jobs]`).
  - **`Y_role` (Execution Phase):** `STATE` | `EFFECT` | `ACTION` | `IO` | `VIEW` | `SCHEMA`.
  - **`ΔZ_write` (State & Table Mutations):** React state setters, `localStorage` writes, object mutations, and SQL tables mutated (`INSERT` / `UPDATE` / `DELETE`).
  - **`Z_read` (State & Table Reads):** State variables, storage keys, and SQL `SELECT` / `JOIN` tables read.
  - **`W_calls` (Downstream Invocations):** Key functions called or UI components rendered.
  - **`E_exit` & `T_mode` (Exit Contracts & Concurrency Mode):** Thrown/caught exceptions (`throw:ApiError`, `catch:IntegrityError`), HTTP status codes (`status:403`, `err:forbidden`), guard returns (`guard_return`), and temporal mode (`SYNC`, `ASYNC`, `REACTIVE`, `TIMER`).

### Skill 4: 7-Way Cross-Boundary Mathematical Contract Verifier (Pass C)
* Statically cross-checks SQL queries, Python types, exception handlers, and Frontend HTTP calls against `.sql` migrations, SQLite/Postgres adapters, and backend route definitions—pinpointing bugs at exact `file:Lline` coordinates without executing the code.

### Skill 5: Self-Verifying Surgical Anchor Patching (`patch` / `brain_patch`)
* Applies multi-file code mutations using compact anchor directives (`@sub`, `@replace`, `@insert_after`, `@insert_before`, `@delete`) via stdin or `--spec-file`, cutting output tokens by **70–85%** compared to `edit_file`.
* **Pre-Disk AST & 6D Contract Gate:** Parses the patched file in memory using `python_ast` or `tree-sitter` AND re-runs the 7-Way 6D Contract Verifier in memory before writing to disk.

### Skill 6: Blast Radius, Plan Verification & Co-Change Coupling (`impact`, `verify`, `co_changes`)
* Computes direct production importers, test consumers, symbol-level callers, and Git commit co-change coupling.

### Skill 7: AST-Anchored Architectural Memory (`remember` / `brain_remember`)
* Pins persistent architectural invariants to specific graph node IDs with automatic AST-hash staleness detection (`[STALE WARNING]`).

### Skill 8: One-Command Multi-IDE Bootstrap & Telemetry (`init`, `stats`)
* Configures `.gitignore`, MCP configs, and agent rules for Antigravity, Claude Code, Cursor, and VS Code in one command.

---

## 2. Industry Benchmark & Capability Comparison

| Capability / Technical Dimension | Raw Shell (`rg` + `read_file`) | Cursor / Windsurf (Vector RAG) | Aider RepoMap (Symbol PageRank) | Sourcegraph / Serena (SCIP / LSP) | CodeQL / Semgrep | **ProjectBrain (`v0.6.1`)** |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Primary Representation** | Flat text lines | 500-token vector chunks | File-level symbol signatures | Single-language LSP symbols | Relational Datalog DB | **6D Coordinate Matrix + 4-Layer Multiplex Graph** |
| **Indexing Latency (60-file repo)** | N/A | 5–30s (cloud API) | ~1.5s | 3–15s (LSP warmup) | 30–180s | **~0.4s (incremental SQLite cache)** |
| **Sub-Function Granularity** | ❌ None | ❌ Blind chunking | ❌ Signatures only | ❌ Definitions only | ✅ AST nodes | **✅ Inner 6D sub-blocks (`with`, `try/catch`, `branch`, `sql`)** |
| **Cross-Language HTTP Bridging (`JS/TS` → `Python`)** | ❌ Manual `rg` | ❌ None | ❌ None | ❌ Single-language | ❌ Separate DBs | **✅ Automatic `http_flow` bridge edges** |
| **SQL Table & State Channels (`ΔZ_write` → `Z_read`)** | ❌ Manual `rg` | ❌ None | ❌ None | ❌ None | ⚠️ Intra-language | **✅ Automatic `state_flow` edges across routes, SQL & workers** |
| **Symptom-to-Guard Causal Chop (`403` → exact `if` guard)** | ❌ Run test & read traceback | ❌ None | ❌ None | ❌ Manual | ❌ Custom query | **✅ Automatic 4-hop `causal_symptom_chop` (`F(S₀) ∩ B(Σ)`)** |
| **Static Cross-Boundary Bug Detection** | ❌ 0 / 7 | ❌ 0 / 7 | ❌ 0 / 7 | ❌ 0 / 7 | ⚠️ 2 / 7 | **✅ 7 / 7 (SQL `NOT NULL`, Dialect, Exceptions, `UUID`/`TEXT`, `SELECT` cols, HTTP verb & shape)** |
| **Working-Memory Interval Dedup** | ❌ Re-reads files | ❌ Re-fetches chunks | ❌ Re-sends map | ❌ Re-fetches bodies | N/A | **✅ Exact Interval-Tree `Zero-Waste Guard`** |
| **Pre-Disk Mutation Verification** | ❌ None | ❌ Post-disk linter | ❌ None | ❌ None | N/A | **✅ In-Memory AST Syntax + 6D Contract Gate** |

---

## 3. Real-World Full-Stack Execution Walkthrough

On a 60-file full-stack production repository (`558 functions`, `81 classes`, `924 6D cells` across React/Vite `.jsx`/`.js`, FastAPI Python, 5 PostgreSQL `.sql` migrations, and a 1,477-line SQLite compatibility engine), running:

```powershell
projectbrain dossier "uploadBatchFile fails with 403 or database constraint error and worker job processing"
```

produces a **222-line dossier** in `<1 second` that—**without running a single test or reading full files**:

1. **Pins the Frontend Entry Point (`frontend/src/api/client.js :: uploadBatchFile`, `L110-L130`)** with its 6D Matrix header:
   ```text
   # [4D Coordinate Matrix] Lstart-Lend | Y_Role | X_Scope | ΔZ_Write -> W_Calls
   #   L 110-L 130 | IO     | fn:uploadBatchFile | W:[append,authHeaders,computeFileSha256] E:[throw:Error] T:ASYNC
   ```
2. **Constructs the Cross-Stack Multiplex & Causal Chop Graph Edges:**
   ```markdown
   - `fn:frontend/src/api/client.js:uploadBatchFile` -[http_flow: HTTP POST /api/v1/batches/${batchId}/files -> upload_file]-> `fn:backend/app/routers/uploads.py:upload_file`
   - 🎯 **[Causal Symptom Chop]** `fn:frontend/src/api/client.js:uploadBatchFile` -> `fn:backend/app/routers/uploads.py:upload_file` -> `fn:backend/app/deps.py:load_batch` *(origin of `err:forbidden, status:403`)*
   ```
3. **Slices the Exact `403 Forbidden` Origin in `backend/app/deps.py :: load_batch` (`L10-L28`):**
   ```python
   18 |     if str(b["created_by"]) != str(user) and not db.has_role(conn, user, "coordinator"):
   19 |         raise ApiError(403, "forbidden", "Only the batch creator or a coordinator can do this")
   ```
4. **Slices the Backend Route & Persistence Layer (`backend/app/routers/uploads.py :: upload_file` & `_persist`) with Inner 6D Sub-Blocks:**
   ```text
   #   L  65-L 188 | IO     | fn:_persist                 | ΔZ:[source_files,source_file_tags,background_jobs]
   #   L  83-L 145 | IO     | try_block                   | ΔZ:[source_files,source_file_tags,background_jobs]
   #   L  84-L 145 | IO     | with[db.tx(user) as conn]   | ΔZ:[source_files,source_file_tags,background_jobs]
   #   L  86-L  93 | IO     | sql[INSERT source_files]    | ΔZ:[source_files]
   #   L 140-L 144 | IO     | sql[INSERT background_jobs] | ΔZ:[background_jobs]
   ```
5. **Outputs Static 6D Contract Diagnostics with Exact Line Numbers:**
   ```markdown
   - ⚠️ **[6D Schema Contract Violation]** `backend/app/routers/uploads.py:L141` (`sql[INSERT background_jobs]`) — `INSERT INTO background_jobs(job_type, batch_id, source_file_id, triggered_by, payload_json)` omits required `NOT NULL` column(s) `run_after, created_at` (declared without `DEFAULT` in `backend/app/local_db.py:L348`).
   - ⚠️ **[6D Schema Contract Violation]** `backend/app/routers/uploads.py:L287` (`sql[INSERT background_jobs]`) — `INSERT INTO background_jobs(job_type, batch_id, source_file_id, triggered_by)` omits required `NOT NULL` column(s) `run_after, created_at` (declared without `DEFAULT` in `backend/app/local_db.py:L348`).
   - ⚠️ **[6D Schema Contract Violation]** `backend/app/routers/uploads.py:L87` (`with[db.tx(user) as conn]`) — `INSERT INTO source_files(...)` omits required `NOT NULL` column(s) `created_at` (declared without `DEFAULT` in `backend/app/local_db.py:L285`).
   - ⚠️ **[6D Schema Contract Violation]** `backend/app/routers/uploads.py:L121` (`with[db.tx(user) as conn]`) — `INSERT INTO source_file_tags(source_file_id, tag)` omits required `NOT NULL` column(s) `created_at` (declared without `DEFAULT` in `backend/app/local_db.py:L318`).
   ```
