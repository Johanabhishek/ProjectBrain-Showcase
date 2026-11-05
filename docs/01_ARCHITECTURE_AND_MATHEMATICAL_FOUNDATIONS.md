# ProjectBrain: Polyglot 6D Multiplex Graph & Mathematical Foundations

> [!IMPORTANT]
> **Architectural Thesis:** ProjectBrain transforms code retrieval from passive lexical/vector lookup into a **polyglot, cross-stack mathematical reasoning & static verification engine** that bridges **Frontend (JS/TS/React) $\leftrightarrow$ Backend (Python/FastAPI/Flask) $\leftrightarrow$ Database Schemas (`.sql` / SQLite / PostgreSQL) $\leftrightarrow$ Background Workers** in `<1 second`.

---

## 1. End-to-End Pipeline Diagram

```mermaid
flowchart TD
    subgraph Indexing["1. Sub-Block 6D Extraction & Schema Indexing"]
        FE["Frontend JS/TS/JSX\n(fetch/axios + response reads)"]
        BE["Backend Python\n(FastAPI/Flask routes, nested callbacks, UUID types)"]
        SQL["SQL Migrations (.sql) & Inline DDL\n(CREATE TABLE, NOT NULL, DEFAULT)"]
        CELLS["6D Behavioral Coordinate Matrix\nC(b) = (X_scope, Y_role, ΔZ_write, Z_read, W_calls, E_exit, T_mode)"]
        FE --> CELLS
        BE --> CELLS
        SQL --> CELLS
    end

    subgraph Multiplex["2. 4-Layer Multiplex Graph G = (V, E1 ∪ E2 ∪ E3 ∪ E4)"]
        L1["Layer 1: AST Calls & Nested Closures (calls / handles)"]
        L2["Layer 2: Shared State & SQL Table Channels (state_flow: ΔZ_write -> Z_read)"]
        L3["Layer 3: Cross-Stack HTTP Bridges (http_flow: fetch/axios -> APIRouter)"]
        L4["Layer 4: Inverse Call/State Transitions"]
        CELLS --> L1 & L2 & L3 & L4
    end

    subgraph Reasoning["3. Mathematical Localization & Verification Engines"]
        PPR["Engine A: Multiplex Personalized PageRank\nπ^(t+1) = (1-α) P^T π^(t) + α v_0"]
        CHOP["Engine B: Causal Program Chop\nX_chop(S_0, Σ) = F_multiplex(S_0) ∩ B(Σ)"]
        SUBMOD["Engine C: Submodular Token Optimizer\nmax ΔI(u | U_cov) / C_unseen(u)^0.55"]
        PASSC["Engine D: 7-Way Cross-Boundary Contract Verifier\nPost(u) ⊨ Pre(v) + Pre-Disk Patch Check"]
        L1 & L2 & L3 & L4 --> PPR & CHOP & PASSC
        PPR & CHOP --> SUBMOD
    end
```

---

## 2. The 5 Core Mathematical Engines

### Engine 1: Fine-Grained 6D Behavioral Coordinate Matrix & SQL Schema Algebra
Every function $\ge 8$ lines in Python, TypeScript, or JavaScript is decomposed into inner structural sub-blocks (`with[...]`, `try_block`, `catch[...]`, `branch[...]`, `sql[...]`, `useEffect[...]`, `case ...`). Each sub-block $b$ is mapped to a 6D coordinate vector plus formal I/O contracts:
$$\mathcal{C}(b) = \bigl(X_{\text{scope}},\; Y_{\text{role}},\; \Delta Z_{\text{write}},\; Z_{\text{read}},\; W_{\text{calls}},\; E_{\text{exit}},\; T_{\text{mode}}\bigr)$$

- **Exit Contract Lattice ($E_{\text{exit}}$):** Captures exceptions (`throw:ApiError`, `catch:IntegrityError`), HTTP status codes (`status:403`, `status:404`, `status:422`), semantic error tags (`err:forbidden`), and guard returns (`guard_return`).
- **Relational Schema Extraction ($\mathcal{S}(T)$):** Parses `.sql` migration files and inline `CREATE TABLE` blocks into column sets $\text{Cols}(T)$ and strict required sets:
  $$\text{Req}(T) = \bigl\{\, c \in \text{Cols}(T) \;\big|\; \text{NOT NULL}(c) \land \neg\text{DEFAULT}(c) \land \neg\text{AUTOINCREMENT}(c) \,\bigr\}$$

---

### Engine 2: 4-Layer Multiplex Graph & Personalized PageRank (`multiplex_ppr`)
Unifies four distinct graph layers into a single column-stochastic Markov transition operator $\mathbf{P}_{\text{multiplex}}$:
1. **`http_flow` ($w_{\text{fwd}} = 1.40$):** Normalizes frontend `fetch`/`axios` URL templates (`/api/v1/batches/${batchId}/files` $\mapsto$ `/api/v1/batches/{*}/files`) and matches them against backend route decorators combined with `APIRouter(prefix=...)` / `Blueprint(url_prefix=...)`.
2. **`state_flow` ($w_{\text{fwd}} = 1.20$):** Connects any function mutating a SQL table or state key ($k \in \Delta Z_{\text{write}}(u)$) to any function reading it ($k \in Z_{\text{read}}(v)$).
3. **`handles` & `calls` ($w_{\text{fwd}} = 1.10, 1.00$):** Direct AST calls, route handlers, and lexically nested callback functions (`on_file_headers` inside `upload_file`).
4. **Inverse edges ($w_{\text{bwd}} \in [0.65, 0.85]$):** Backward edges across all layers.

Starting from query seed vector $\vec{v}_0$, `multiplex_ppr` runs $T = 12$ power iterations with restart probability $\alpha = 0.30$:
$$\vec{\pi}^{(t+1)} = (1 - \alpha)\,\mathbf{P}_{\text{multiplex}}^{\top}\,\vec{\pi}^{(t)} + \alpha\,\vec{v}_0$$

---

### Engine 3: Causal Program Chop across the Multiplex Graph (`causal_symptom_chop`)
When a prompt mentions an error symptom $\Sigma$ (e.g., `403`, `forbidden`, `404`, `409`, `422`), ProjectBrain computes the **Causal Program Chop**—the intersection of the 4-hop forward multiplex execution cone from entry seeds $S_0$ and the set of nodes whose local exit contracts emit $\Sigma$:
$$\mathcal{X}_{\text{chop}}(S_0, \Sigma) = \mathcal{F}_{\text{multiplex}}^{\le 4}(S_0) \;\cap\; \bigl\{\, v \in V \;\big|\; E_{\text{exit}}^{\text{local}}(v) \cap \Sigma \neq \emptyset \,\bigr\}$$
It reconstructs the exact cross-stack causal chain $s_0 \xrightarrow{\text{http\_flow}} u_1 \xrightarrow{\text{calls}} \dots \xrightarrow{\text{calls}} v^*$ and slices the exact guard in $v^*$ into the dossier.

---

### Engine 4: Submodular Marginal Information Gain-per-Token Optimizer
Given candidate slices $\mathcal{C}_{\text{rem}}$, already-covered 6D behavioral features $\mathcal{U}_{\text{cov}}$, and exact unseen line token cost $C_{\text{unseen}}(u)$ from the Interval-Tree Working-Memory Ledger, the dossier greedily selects at each step:
$$u^* = \arg\max_{u \in \mathcal{C}_{\text{rem}}} \frac{\pi_{\text{PPR}}(u) \cdot \bigl(1 + \sum_{f \in F(u) \setminus \mathcal{U}_{\text{cov}}} \omega_f\bigr)}{\bigl(\max(12,\, C_{\text{unseen}}(u))\bigr)^{0.55}}$$

---

### Engine 5: 7-Way Cross-Boundary Contract Verifier & Pre-Disk Patch Verification
Pass C checks **7 formal invariants** statically during `dossier` compilation AND in memory during `projectbrain patch` (even in `apply=False` dry-run mode before touching disk):

| # | Diagnostic Tag | Mathematical Invariant Checked | Bug Class Caught Statically |
| :--- | :--- | :--- | :--- |
| **1** | `[6D Schema Contract Violation]` | $\text{Req}(T) \setminus \text{Cols}_{\text{INSERT}}(q) = \emptyset$ | `INSERT INTO` omitting `NOT NULL` columns lacking `DEFAULT` in `.sql` / `local_db.py` |
| **2** | `[6D SQL Dialect Mismatch]` | $\Phi_{\text{query}}(q) \subseteq \Phi_{\text{adapter}}(\text{SQLite})$ | PostgreSQL `interval '...'`, `make_interval`, `= ANY(%s)` against untranslated `sqlite3` |
| **3** | `[6D Exception Contract Mismatch]` | $\Delta Z_{\text{write}} \neq \emptyset \implies \text{catch:IntegrityError} \in E_{\text{exit}}$ | Catching `psycopg.UniqueViolation` without `sqlite3.IntegrityError` |
| **4** | `[6D Type Disjointness Violation]` | $\tau(p_{\text{UUID}}) \cap \tau(\text{row}[k]_{\text{TEXT}}) \neq \emptyset$ | Comparing `UUID` parameter directly to SQLite `TEXT` `row["col"]` without `str()`/`UUID()` |
| **5** | `[6D Producer-Consumer SQL Shape Violation]` | $\text{Post}(\texttt{SELECT}) \models \text{Pre}(\text{row}[k])$ | Reading `row["col"]` when `col` was omitted from `SELECT c1, c2 FROM T` |
| **6** | `[6D HTTP Route Method Mismatch]` | $\text{Method}_{\text{FE}}(u) \in \text{Methods}_{\text{BE}}(\text{url})$ | Frontend `fetch`/`axios` calling `DELETE`/`PUT` on a `POST`-only backend route |
| **7** | `[6D Cross-Stack HTTP Shape Violation]` | $\text{Post}_{\text{BE}}(v) \models \text{Pre}_{\text{FE}}(u)$ | Frontend reading `data.prop` when backend handler's `return {...}` dict omits `prop` |
