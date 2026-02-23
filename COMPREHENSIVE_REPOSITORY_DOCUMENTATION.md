# Comprehensive Repository Documentation

## Document metadata

- Repository: `pegasystems/pega-datascientist-tools` (local checkout)
- Package: `pdstools`
- Document date: 2026-02-23
- Source of truth: Repository contents only (code, configuration, workflows, tests, Git metadata)

---

## 1. Executive summary (non-technical)

Pega Data Scientist Tools is an open-source analytics toolkit that helps data science and decisioning teams understand, validate, and improve decisioning and predictive model behavior in Pega environments. It provides reusable Python APIs, interactive applications, and report-generation pipelines to make operational AI model monitoring more transparent and easier to act upon.

The repository serves three practical business goals:

1. **Operational visibility** into Adaptive Decision Manager model quality, predictor behavior, and performance trends.
2. **Decisioning optimization** through diagnostics for Value Finder, Decision Analyzer, Interaction History, and Impact Analyzer data.
3. **Platform integration** with Pega Infinity APIs for Prediction Studio, model management, and notifications.

Primary users are:

- Data scientists and applied machine learning practitioners working with Pega AI.
- Decisioning specialists responsible for Next-Best-Action operations.
- Analytics engineers and technical product owners maintaining model governance workflows.

The project has the characteristics of a mature open-source technical product:

- Stable packaging and release process.
- Broad automated test coverage and multi-platform continuous integration.
- Structured documentation generation and examples.
- Clear contribution and security reporting pathways.

At the same time, it still carries active evolution signals:

- Development status classifier is Beta.
- Some user interface pages are explicitly marked unfinished.
- There are known technical debt markers and version drift in selected documentation metadata.

Overall readiness is strong for technical teams with Python proficiency and Pega domain context, with clear opportunities for hardening around security defaults, test coverage boundaries, and governance automation.

---

## 2. High-level technical overview

### 2.1 What the system does

The repository delivers:

- A Python package (`pdstools`) for data ingestion, transformation, analytics, and plotting.
- A command line interface (`pdstools`) for launching Streamlit applications.
- Two primary Streamlit applications:
  - Health Check
  - Decision Analyzer
- Quarto-based report generation for health checks, model reports, and global explanations.
- An Infinity client SDK for authenticated interaction with Pega APIs.

### 2.2 Main features and components

- **Adaptive Decision Manager Datamart analytics** (`pdstools.adm`)
  - Model and predictor snapshot ingestion.
  - Aggregation and diagnostics.
  - Plotly visualizations.
  - Report generation (HTML and Excel).
- **Interaction History analytics** (`pdstools.ih`)
  - Outcome summarization and sequence analysis.
  - Pointwise Mutual Information workflows.
- **Value Finder analytics** (`pdstools.valuefinder`)
  - Propensity threshold analysis and funnel diagnostics.
- **Prediction Studio monitoring** (`pdstools.prediction`)
  - Prediction-level and channel-level trend metrics.
- **Impact Analyzer analytics** (`pdstools.impactanalyzer`)
  - Experimental control group lift summaries.
- **Global explanations pipeline** (`pdstools.explanations`)
  - Batch preprocessing with DuckDB.
  - Contextual and overall contribution aggregation.
  - Plot and report generation.
- **Decision Analyzer engine** (`pdstools.decision_analyzer`)
  - Stage-aware decision filtering, aggregation, ranking simulation, and what-if lever analysis.
- **Infinity API client** (`pdstools.infinity`)
  - Knowledge Buddy and Prediction Studio integrations with version-aware resource loading.
- **I/O and utility layer** (`pdstools.pega_io`, `pdstools.utils`)
  - Dataset import, caching, schema normalization, type parsing, reporting helpers, and optional dependency loading.

### 2.3 High-level architecture

The repository follows a layered analytical architecture:

1. **Ingestion layer**: reads local files, zipped exports, partitioned dataflow outputs, selected remote resources, and API responses.
2. **Normalization layer**: applies schema typing, date parsing, field normalization, and context extraction.
3. **Domain analytics layer**: computes aggregates and derived indicators per domain (ADM, IH, Prediction, Value Finder, Decision Analyzer, Explanations).
4. **Presentation layer**: exposes Plotly figures, Streamlit applications, and Quarto reports.
5. **Integration layer**: Infinity API client and S3 connectors.

### 2.4 Technology stack with versions and constraints

Core technologies observed in `pyproject.toml` and lock/config files:

- Python `>=3.9`
- `polars==1.34.0` (core data frame engine)
- `typing_extensions`
- Optional analytical and visualization ecosystem:
  - `plotly[express]>=6.0`
  - `streamlit>=1.45`
  - `duckdb`
  - `pyarrow`
  - `great_tables>=0.13`
  - `quarto`
  - `papermill`
  - `xlsxwriter>=3.0`
- API and model integration stack:
  - `httpx`
  - `pydantic`
  - `anyio`
  - `aioboto3`
  - `scikit-learn>=1.6.1`
  - `skl2onnx>=1.19.1`
  - `onnx>=1.18,<1.20`
  - `onnxruntime==1.18.1` for Python `<3.10`, `onnxruntime>=1.22` for Python `>=3.10`
- Documentation and developer tooling:
  - Sphinx, nbsphinx, Furo, MyST, sphinx-autoapi
  - `pre-commit`
  - `ruff`
  - `nb-clean`
- Dependency lock model:
  - `uv.lock` present with pinned package versions and hashes.

### 2.5 Third-party integrations and libraries

- Pega Infinity REST APIs (Prediction Studio and Knowledge Buddy endpoints).
- Amazon Simple Storage Service support via `aioboto3`.
- Codecov integration for coverage reporting in continuous integration.
- GitHub Actions for testing, documentation deployment, and release automation.
- PyPI publishing workflow for package distribution.

### 2.6 Design patterns used

- **Namespace composition pattern** (for example `ADMDatamart.plot`, `ADMDatamart.aggregates`, `ADMDatamart.generate`).
- **Lazy evaluation pattern** using Polars LazyFrame for scalable transformation pipelines.
- **Optional dependency pattern** through `LazyNamespace` and `MissingDependenciesException`.
- **Versioned API resource pattern** in Infinity Prediction Studio (`v24_1`, `v24_2` loaders).
- **Factory/classmethod ingestion pattern** (`from_ds_export`, `from_dataflow_export`, `from_pdc`, `from_mock_data`).

---

## 3. Repository structure and metadata

## 3.1 Top-level structure

- `python/`: primary package, documentation source, and tests.
- `data/`: packaged sample datasets and fixtures.
- `examples/`: notebooks and scripts demonstrating workflows.
- `.github/`: continuous integration, release workflows, issue templates, dependency automation.
- `.devcontainer/`: reproducible development environment metadata.
- `README.md`, `CONTRIBUTING.md`, `SECURITY.md`, `pyproject.toml`, `uv.lock`: governance, packaging, and setup metadata.

### 3.2 Repository activity and commit patterns

Static Git metadata in this checkout indicates:

- Total commits observed: **1625**
- Earliest commit timestamp observed: **2018-03-14**
- Latest commit timestamp observed: **2025-11-03**
- Total tags observed: **78**
- Latest tags observed: `V4.5.2`, `V4.5.1`, `V4.5.0`, `V4.4.5`
- Merge commits observed: **297**

Top contributors by commit count in local history (sample):

- Otto Perdeck
- Stijn Kas
- perdo
- yusufuyanik1
- Uyanik, Yusuf

Interpretation:

- Release cadence is active and frequent.
- Development appears collaborative with multiple long-term contributors.
- The project has sustained multi-year evolution.

---

## 4. Folder-level and module-level analysis

## 4.1 Top-level folder purpose

### `.github/`

- Contains seven workflow files covering tests, docs, release, auto-tagging, and package publishing.
- Includes Dependabot configuration (`dependabot.yaml`) with weekly update checks for `uv`.
- Includes issue templates for bug and feature reporting.

### `.devcontainer/`

- Defines a Python 3.11 development container image.
- Installs editor extensions and optional tools (Quarto, Pandoc).
- Configures default app startup command.

### `python/pdstools/`

- Core package implementing all analytics, application, API, and utility logic.

### `python/tests/`

- Test suite spanning core domains, integrations, reports, and explanations.

### `python/docs/`

- Sphinx and notebook-driven documentation configuration and build scripts.

### `data/`

- Reference and sample datasets for local experimentation and tests.

### `examples/`

- Notebook and shell-script usage demonstrations by analytical domain.

### `images/`

- Branding and documentation image assets.

## 4.2 Module-level analysis

| Module | Problem solved | Interactions | Strengths | Limitations and assumptions |
|---|---|---|---|---|
| `adm` | Model and predictor datamart analysis | Uses `pega_io`, `utils`, `reports` | Rich domain analytics, charts, report exports | Heavy data operations can require memory tuning |
| `ih` | Interaction History outcome and sequence analysis | Uses shared utilities and Plotly | Includes advanced Pointwise Mutual Information path analysis | Outcome label assumptions are predefined |
| `valuefinder` | Offer quality and threshold analysis | Uses shared schema/type and plotting tools | Clear stage-level analytics and threshold workflows | Assumes Value Finder schema compatibility |
| `prediction` | Prediction Studio monitoring analytics | Uses CDH guideline mapping and derived metrics | Channel-level trend diagnostics and validity checks | Some strict validity rules may exclude marginal datasets |
| `impactanalyzer` | Experimental lift and control-group summaries | Parses PDC JSON and aggregates by channel | Useful comparative business lift summaries | Input assumptions depend on PDC output structure |
| `explanations` | Global predictor contribution extraction and reporting | Uses DuckDB, Polars, Quarto templates | Context-aware batch processing and report generation | Requires preprocessing resources and file organization |
| `decision_analyzer` | Decision-level stage filtering, ranking simulation, what-if analysis | Uses app pages and table definitions | Strong exploratory analysis workflows for arbitration logic | Some pages and workflows remain under active refinement |
| `infinity` | Authenticated Pega API client | Depends on `httpx`, `pydantic`, internal resource registry | Version-aware resources, typed response models, pagination support | No server implementation; client-only responsibilities |
| `pega_io` | File import, zip handling, caching, S3 integration, anonymization | Used by most domain modules | Broad source format support and helper abstractions | Some remote operations rely on optional packages and external connectivity |
| `utils` | Shared query, schema, date parsing, reporting, optional dependency handling | Imported across all modules | Centralized reusable primitives | Large utility surface increases coupling risk |
| `app` | Streamlit user interfaces (Health Check and Decision Analyzer) | Orchestrates domain classes | Rapid interactive workflows for non-coding users | Streamlit state complexity and some unfinished pages |

---

## 5. Detailed codebase documentation

## 5.1 Core classes and logical flow

### `ADMDatamart` (`python/pdstools/adm/ADMDatamart.py`)

- **Inputs**:
  - Model snapshot LazyFrame.
  - Predictor snapshot LazyFrame.
  - Optional query filters and key extraction options.
- **Primary flow**:
  1. Validate and normalize model data.
  2. Compute first action appearance dates.
  3. Validate and normalize predictor data.
  4. Join latest snapshots into `combined_data`.
  5. Expose plot, aggregate, AGB, report, guideline, and binning namespaces.
- **Outputs**:
  - Normalized LazyFrames.
  - Derived summaries and visual assets.
- **Dependencies**:
  - Polars, schema definitions, utilities, report helpers.
- **Error handling**:
  - Raises validation exceptions for missing schema expectations and invalid query results.
- **Performance-sensitive zones**:
  - Snapshot joins, schema inference, and collect-heavy operations in downstream methods.

### `DecisionAnalyzer` (`python/pdstools/decision_analyzer/decision_data.py`)

- **Inputs**:
  - Raw Explainability Extract or Decision Analyzer data.
  - Stage granularity, sample size, optional mandatory ranking expression.
- **Primary flow**:
  1. Determine extract type.
  2. Validate required columns against table definitions.
  3. Rename and cast types.
  4. Compute ranking and stage fields.
  5. Build cached pre-aggregated filter and remaining views.
  6. Provide analytical methods (funnel, distribution, sensitivity, lever simulation).
- **Outputs**:
  - Stage-aware aggregates and simulation data for Streamlit pages.
- **Error handling**:
  - Validation warnings and explicit exceptions for missing fields.
- **Performance-sensitive zones**:
  - Sampling, stage rollups, and repeated ranking under what-if scenarios.

### `Infinity` and internal API clients (`python/pdstools/infinity`)

- **Inputs**:
  - Basic credentials or OAuth client credentials.
  - Optional explicit Pega version.
- **Primary flow**:
  1. Initialize `httpx` clients and authentication.
  2. Optionally infer Pega version via repository endpoint.
  3. Instantiate resource clients dynamically by version.
  4. Dispatch endpoint operations and map errors.
- **Outputs**:
  - JSON dictionaries, typed response models, paginated resource iterables.
- **Error handling**:
  - Custom exception hierarchy for timeout, connection, and API errors.

### `Reports` namespaces (`adm` and `explanations`)

- **Inputs**:
  - Prepared data and report parameters.
- **Primary flow**:
  1. Serialize input and runtime parameters.
  2. Copy Quarto resources to temporary workspace.
  3. Execute Quarto render command.
  4. Emit output files and optional zipped artifacts.
- **Dependencies**:
  - Quarto, Pandoc (for selected flows), YAML, filesystem tools.

## 5.2 File and data ingestion patterns

The repository supports multiple ingestion routes:

- Dataset exports (`read_ds_export`) from csv, json, zip, parquet, feather, ipc.
- Dataflow outputs with caching and incremental anti-join logic (`read_dataflow_output`).
- PDC JSON transformations for Impact Analyzer and Prediction.
- Optional S3 asynchronous downloads with temporary local caching.
- Streamlit file upload and direct path input options.

## 5.3 Error handling mechanisms

Observed patterns:

- Domain-level `ValueError` for invalid input and empty query outcomes.
- Custom API exception mapping in Infinity internals.
- Streamlit error capture with downloadable debug logs in Health Check pages.
- Explicit type and folder validation in Explanations preprocessing and aggregate loading.

## 5.4 Security considerations inside code paths

- Credentials can be sourced from explicit arguments or environment variables for Infinity basic authentication.
- OAuth token refresh and reuse logic is implemented in `PegaOAuth`.
- No hard-coded production secrets were found in repository code.
- Security-sensitive caveats are documented in section 15.

## 5.5 Performance-sensitive areas

- LazyFrame to eager conversion boundaries (`collect`) in reporting and user interface flows.
- High-cardinality grouping and list aggregation in Decision Analyzer and Explanations.
- Large notebook/report rendering operations through Quarto.
- Multi-file dataflow import and caching behavior for partitioned exports.

---

## 6. Architecture documentation

## 6.1 Textual system architecture diagram

```text
[Data Sources]
  |- Pega dataset exports (zip/json/csv/parquet)
  |- Pega dataflow partition files
  |- PDC JSON exports
  |- Optional S3 objects
  |- Infinity REST API responses
        |
        v
[Ingestion + Normalization Layer]
  |- pdstools.pega_io.File
  |- pdstools.pega_io.S3
  |- pdstools.utils.cdh_utils
  |- Schema modules (adm/valuefinder/decision_analyzer)
        |
        v
[Domain Analytics Layer]
  |- ADMDatamart (+ Aggregates/Plots/Reports/BinAggregator/AGB)
  |- IH (+ Aggregates/Plots)
  |- ValueFinder (+ Aggregates/Plots)
  |- Prediction (+ Plots)
  |- ImpactAnalyzer (+ Plots)
  |- Explanations (+ Preprocess/Aggregate/Plots/Reports)
  |- DecisionAnalyzer (+ Plot engine)
        |
        +----------------------+
        |                      |
        v                      v
[Presentation Layer]      [Integration Layer]
  |- Streamlit apps          |- Infinity API client
  |- Quarto reports          |- Versioned resources
  |- Plotly figures          |- Pydantic models
```

## 6.2 Data flow explanation

### Flow A: Health Check

1. User imports model and predictor snapshots via UI or file path.
2. `ADMDatamart` validates schema, applies optional filtering, builds combined latest snapshot.
3. Aggregation and plotting logic populate report sections.
4. Quarto report templates render to output HTML.
5. Optional Excel exports are generated with sheet-size safety checks.

### Flow B: Decision Analyzer

1. User supplies Explainability Extract or Decision Analyzer dataset.
2. `DecisionAnalyzer` standardizes schema and ranking.
3. Cached pre-aggregates support dashboard, funnel, sensitivity, and leverage pages.
4. Interactive Streamlit pages query and visualize aggregated results.

### Flow C: Infinity API client

1. Caller initializes `Infinity` via basic or OAuth credentials.
2. Version inference loads compatible resource class.
3. Resource methods call endpoint wrappers and return structured results.

## 6.3 Deployment architecture

No direct container-orchestrated production deployment manifests are included in this repository. Observed deployment/runtime model:

- Library install through package managers (`uv`, `pip`).
- Local or hosted Streamlit execution through CLI.
- GitHub-hosted documentation deployment to GitHub Pages.
- PyPI release on tag workflows.
- Optional local development container via devcontainer configuration.

## 6.4 Configuration management

- Python packaging and extras are defined in `pyproject.toml`.
- Full dependency lock is captured in `uv.lock`.
- Workflow behavior is configured in `.github/workflows/*.yml`.
- Report execution parameters are injected through generated YAML files.
- Runtime behavior is partially configured through environment variables (documented in section 11).

## 6.5 Scalability considerations

Positive indicators:

- Extensive use of Polars LazyFrame operations for deferred computation.
- Partitioned dataflow ingestion and cache strategy.
- Batched DuckDB query execution for explanations.

Limitations:

- Some flows collect to memory for plotting/reporting.
- Streamlit state and interaction-heavy computations can become expensive at very large scale.
- No dedicated distributed execution orchestration is present in repository code.

---

## 7. API documentation (applicable client-side API wrappers)

Important clarification: this repository does **not** implement a server-side REST service. It provides a **client SDK** for Pega APIs.

## 7.1 Authentication

Supported modes in `Infinity`:

1. **Basic authentication**
   - Constructor: `Infinity.from_basic_auth(...)`
   - Can read from environment variables:
     - `PEGA_BASE_URL`
     - `PEGA_USERNAME`
     - `PEGA_PASSWORD`
2. **OAuth2 client credentials**
   - Constructor: `Infinity.from_client_credentials(file_path=...)`
   - Uses `PegaOAuth` with token caching and refresh.

## 7.2 Endpoint map (observed)

### Knowledge Buddy

- `POST /prweb/api/knowledgebuddy/v1/question`
- `PUT /prweb/api/knowledgebuddy/v1/question/feedback`

### Prediction Studio (selected)

- `GET /prweb/api/PredictionStudio/v3/predictions/repository`
- `GET /prweb/api/PredictionStudio/v1/models`
- `GET /prweb/api/PredictionStudio/V2/predictions`
- `GET /prweb/api/PredictionStudio/v1/models/{model_id}`
- `GET /prweb/api/PredictionStudio/v3/predictions/{prediction_id}`
- `GET /prweb/api/PredictionStudio/v2/predictions/{prediction_id}/metric/{metric}`
- `POST /prweb/api/PredictionStudio/v1/datamart/export`
- `GET /prweb/api/PredictionStudio/v1/datamart/export/{reference_id}`
- `POST /prweb/api/PredictionStudio/v1/model` (model upload)
- `PATCH /prweb/api/PredictionStudio/v4/...` endpoints for champion/challenger operations

## 7.3 Request and response model structure

Examples:

- Knowledge Buddy response is normalized into `BuddyResponse` model with fields such as:
  - `question_id`
  - `answer`
  - `status`
  - `search_results`
- Prediction Studio list calls use `PaginatedList` abstraction and can be materialized as Polars DataFrames.

## 7.4 Usage example

```python
from pdstools.infinity import Infinity

client = Infinity.from_basic_auth(
    base_url="https://my-infinity.example.com/prweb",
    user_name="operator",
    password="secret",
    pega_version="24.2",
)

repo = client.prediction_studio.repository()
predictions_df = client.prediction_studio.list_predictions(return_df=True)
```

---

## 8. DevOps and continuous integration / continuous delivery documentation

## 8.1 Build and test process

Primary workflow: `Python tests.yml`

- Triggered on pushes to `master` and `release/**`, and qualifying pull request events.
- Uses matrix across operating systems and Python versions.
- Uses `uv` for Python installation and dependency synchronization.
- Executes `pytest` with coverage, excluding selected tests.
- Uploads coverage to Codecov.

## 8.2 Specialized workflows

- `Healthcheck tests.yml`: dedicated Health Check test execution with Quarto and Pandoc installation.
- `Docs check.yml`: validates documentation build on pull requests.
- `Docs deploy.yml`: builds and deploys documentation to GitHub Pages on master and tags.
- `create-release.yml`: interactive version bump and release branch / pull request orchestration.
- `auto-tag-on-merge.yml`: creates tags on release pull request merge and drafts major/minor releases.
- `Python release.yml`: builds and publishes package artifacts to PyPI on tag push.

## 8.3 Environments

Repository-defined environment patterns:

- **Development**: local machine or devcontainer (`mcr.microsoft.com/devcontainers/python:0-3.11`).
- **Continuous integration**: GitHub-hosted runners.
- **Documentation deployment**: GitHub Pages.
- **Package distribution**: PyPI.

No explicit staging or production infrastructure manifests are defined in this repository.

## 8.4 Observability

Observed observability mechanisms:

- Python logging across analytical modules and utilities.
- Workflow logs in GitHub Actions.
- Streamlit error-log download in Health Check report page.

Missing from repository:

- Dedicated metrics pipeline.
- Alerting configuration.
- Structured tracing instrumentation.

---

## 9. Installation and setup guide

## 9.1 Prerequisites

- Python 3.9 or newer.
- `uv` package manager recommended.
- For Health Check and docs/report generation:
  - Quarto
  - Pandoc
- Optional dependencies depending on features used (API, app, onnx, explanations, S3).

## 9.2 Basic installation

```bash
uv sync
```

## 9.3 Full-feature installation

```bash
uv sync --extra all
```

## 9.4 Development installation

```bash
uv sync --extra dev --extra tests --extra docs --extra all
pre-commit install
```

## 9.5 Run applications

Health Check:

```bash
uv run pdstools run health_check
```

Decision Analyzer:

```bash
uv run pdstools run decision_analyzer
```

## 9.6 Run tests

```bash
uv run pytest python/tests
```

With coverage:

```bash
uv run pytest python/tests --cov=./python/pdstools --cov-report=xml
```

## 9.7 Build documentation locally

```bash
cd python/docs
uv run make html
```

---

## 10. Testing documentation

## 10.1 Test types included

- Unit tests for utilities and domain classes.
- Integration-like tests for report generation and API clients.
- Notebook execution scenario tests (`testbook`) for documentation examples.
- Endpoint and authentication behavior tests for Infinity client.
- Domain-specific tests for explanations, prediction studio, value finder, and anonymization.

## 10.2 Coverage and exclusions

Coverage configuration (`python/tests/.coveragerc`) omits:

- `python/pdstools/app/*`
- `python/pdstools/ih/*`
- `**/__init__.py`
- `python/tests/test_healthcheck.py`

Main Python test workflow ignores:

- `python/tests/test_healthcheck.py`
- `python/tests/test_ADMTrees.py`

Health Check tests are validated in a separate workflow. ADMTrees tests are present in repository but excluded in the primary matrix workflow.

## 10.3 How to execute tests

- General suite: `uv run pytest python/tests`
- Targeted file: `uv run pytest python/tests/test_end_to_end.py`
- Health Check only: `uv run pytest python/tests/test_healthcheck.py`

## 10.4 Known testing gaps and risks

- Streamlit applications are mostly excluded from coverage.
- Interaction History module is excluded from coverage configuration.
- ADMTrees regression confidence in default pipeline is limited due workflow exclusion.
- No dedicated performance benchmark suite is visible.

---

## 11. Configuration and environment variables

## 11.1 Runtime environment variables in code

| Variable | Location | Purpose | Default |
|---|---|---|---|
| `PEGA_BASE_URL` | Infinity base client | Basic auth base URL fallback | None |
| `PEGA_USERNAME` | Infinity base client | Basic auth username fallback | None |
| `PEGA_PASSWORD` | Infinity base client | Basic auth password fallback | None |
| `MODEL_CONTEXT_LIMIT` | Explanations preprocess | Cap number of contexts handled | `2500` |
| `QUERY_BATCH_LIMIT` | Explanations preprocess | Context query batch size | `10` |
| `FILE_BATCH_LIMIT` | Explanations preprocess | File-level batch grouping | `10` |
| `MEMORY_LIMIT` | Explanations preprocess | DuckDB memory cap in gigabytes | `8` |
| `THREAD_COUNT` | Explanations preprocess | DuckDB thread count | `4` |
| `PROGRESS_BAR` | Explanations preprocess | Enable DuckDB progress bar (`1` or `0`) | `0` |

## 11.2 Continuous integration secrets and environment settings

| Item | Workflow usage |
|---|---|
| `secrets.GITHUB_TOKEN` | GitHub API operations and token propagation |
| `secrets.codecov_token` | Coverage upload in test workflow |
| `GH_TOKEN` | Release pull request and release creation workflow steps |

## 11.3 Configuration files

- `pyproject.toml`: package metadata, dependencies, extras, scripts, pytest options.
- `uv.lock`: dependency lock and hashes.
- `.pre-commit-config.yaml`: pre-commit quality gates.
- `.devcontainer/devcontainer.json`: development container settings.
- `.github/workflows/*.yml`: automation behavior.

---

## 12. Data model documentation

## 12.1 Main entities

### ADM model snapshot (`ADMModelSnapshot`)

Representative fields:

- Identification: `pyModelID`, `pyConfigurationName`, `pyName`
- Context: `pyIssue`, `pyGroup`, `pyChannel`, `pyDirection`, optional `pyTreatment`
- Metrics: `pyPerformance`, `pySuccessRate`, `pyResponseCount`, positives/negatives
- Time: `pySnapshotTime`, `pxSaveDateTime`, `pxCommitDateTime`

### ADM predictor binning snapshot (`ADMPredictorBinningSnapshot`)

Representative fields:

- Link: `pyModelID`
- Predictor dimensions: `pyPredictorName`, `pyType`, `pyEntryType`
- Bin fields: `pyBinIndex`, bounds, symbols, positives, negatives, response counts
- Performance metrics: `pyPerformance`, `pyLift`, `pyZRatio`

### Value Finder entity (`pyValueFinder`)

- Keys and context: direction, subject, issue, group, channel, name.
- Stage enum: Eligibility, Applicability, Suitability, Arbitration.
- Propensity and priority metrics.
- Customer and decision time fields.

### Decision Analyzer / Explainability Extract table definitions

- Mapped through explicit field dictionaries with default-required columns and target data types.
- Supports extraction type detection and schema-normalized rename/cast.

### Prediction monitoring records

- Derived from snapshots into normalized structures containing:
  - test/control/NBA positives and negatives
  - click-through rate variants
  - lift and validity flags

### Explanations aggregate schema

Representative fields:

- `partition` (context key bundle)
- predictor identity and type
- contribution metrics (raw, absolute, weighted, min, max)
- frequency and binned value descriptors

## 12.2 Relationships between entities

- `ModelID` links ADM model snapshots to predictor snapshots.
- Prediction summaries derive from grouped records keyed by prediction model identifiers.
- Decision Analyzer records group by interaction and stage to produce filter and remaining views.
- Explanations partitions encode context dictionaries that map contribution summaries to model context.

## 12.3 Example object patterns

- API response model example:
  - Knowledge Buddy returns `question_id`, `answer`, `status`, optional `search_results`.
- Report parameter object:
  - Quarto parameter YAML includes file paths, selected model identifiers, and display metadata.

---

## 13. Usage guide and user documentation

## 13.1 Typical user workflows

### Workflow A: Run Health Check from exported data

1. Export model and predictor snapshots from Pega.
2. Load files through Streamlit Health Check import page or Python API.
3. Apply optional filters.
4. Generate health check HTML report and optional Excel workbook.

### Workflow B: Explore Decision Analyzer data

1. Import Decision Analyzer or Explainability Extract dataset.
2. Review global dashboard and funnel pages.
3. Analyze sensitivity and win/loss pages.
4. Run business lever what-if simulations.

### Workflow C: Use Infinity client for model operations

1. Initialize authenticated Infinity client.
2. List predictions and models.
3. Inspect metrics or notifications.
4. Trigger datamart exports or upload models for champion/challenger operations.

## 13.2 Command line usage

- `pdstools run`
- `pdstools run health_check`
- `pdstools run decision_analyzer`

The command internally delegates to Streamlit and appends upload-size configuration if absent.

## 13.3 Python usage snippets

```python
from pdstools import ADMDatamart

dm = ADMDatamart.from_ds_export(base_path="/path/to/export")
summary = dm.aggregates.overall_summary().collect()
fig = dm.plot.bubble_chart()
```

```python
from pdstools.decision_analyzer.decision_data import DecisionAnalyzer
from pdstools.decision_analyzer.data_read_utils import read_data

raw = read_data("/path/to/decision/analyzer/files")
da = DecisionAnalyzer(raw_data=raw, level="StageGroup", sample_size=50000)
```

---

## 14. Code quality and maintainability assessment

## 14.1 Strengths observed

- Clear modular domain boundaries.
- Extensive typed schema usage and explicit casting logic.
- Strong use of lazy data processing for large analytical datasets.
- Meaningful test presence across core domains.
- Well-defined automation for tests, docs, and release management.

## 14.2 Coding standards and tooling

- Pre-commit hooks include whitespace checks, YAML checks, Ruff lint and formatting, notebook cleanup.
- Repository includes package lock file and extras grouping.
- Sphinx auto API documentation is configured.

## 14.3 Areas for improvement

1. **Coverage scope consistency**: application and selected modules are currently omitted.
2. **Documentation metadata drift**: `python/docs/source/conf.py` release field is set to `4.0.0` while package version is `4.3.6`.
3. **Technical debt concentration**: multiple TODO markers and unfinished Streamlit pages.
4. **Utility module growth**: `cdh_utils.py` has broad responsibilities that could be split into smaller domains.
5. **Exception consistency**: mixture of generic exceptions and custom exceptions in some paths.

## 14.4 Refactoring opportunities

- Extract dedicated modules for date parsing, statistics, and query composition currently grouped in large utility files.
- Standardize API client endpoint construction and response typing.
- Isolate report execution shell invocation into hardened adapter with stricter parameter validation.
- Consolidate duplicate helper logic between Streamlit utility modules.

---

## 15. Security assessment (repository-based only)

## 15.1 Hard-coded secrets check

Repository scan did not reveal obvious hard-coded credential literals in source paths.

## 15.2 Dependency and supply-chain posture

- Dependency lock file includes hashes.
- Dependabot is configured weekly for the `uv` ecosystem.
- PyPI publishing is automated via tagged release workflows.

## 15.3 Security-relevant risks identified

1. **Transport security default risk in API client constructors**
   - Several API constructor signatures default `verify` to `False` (or equivalent unsecured behavior) in certain paths.
   - Recommendation: default to certificate verification enabled and force explicit opt-out.

2. **Use of dynamic `eval` in ADMTrees**
   - `eval` usage appears in tree split parsing/scoring logic.
   - Even if inputs are expected from trusted model exports, this pattern increases risk surface.
   - Recommendation: replace with explicit operator mapping and safe comparisons.

3. **Subprocess invocation in report generation**
   - Quarto command execution is expected behavior, but all user-influenced path values should be sanitized and constrained.

4. **Runtime credential handling**
   - Environment-variable credential sourcing is practical but requires secure execution environment discipline.

## 15.4 Access control concerns

- As a library client, this repository delegates authorization to external Pega systems.
- Fine-grained access control is therefore outside this codebase and depends on Pega operator and OAuth setup.

---

## 16. Feature roadmap suggestions

## 16.1 Near-term (high value)

1. Make secure transport verification the default across all API constructors.
2. Remove `eval` from ADMTrees and replace with safe deterministic operators.
3. Expand continuous integration to include ADMTrees tests in at least one controlled lane.
4. Add automated checks for documentation version consistency with package version.
5. Promote unfinished Decision Analyzer pages into feature-flagged modules or remove from shipped navigation.

## 16.2 Medium-term

1. Introduce benchmark suite for large-dataset scenarios and report generation timings.
2. Add optional structured telemetry hooks for long-running transforms and report renders.
3. Improve schema evolution tooling with explicit migration and deprecation warnings.
4. Introduce stricter static typing and lint configuration in `pyproject.toml`.
5. Expand notebook scenario tests to include more examples and failure diagnostics.

## 16.3 Long-term

1. Offer a plugin architecture for custom domain-specific analytics namespaces.
2. Add remote object store adapters beyond current S3 scope.
3. Build a formal compatibility matrix between Pega versions and Infinity resource capabilities.
4. Deliver enterprise-grade governance bundle:
   - security baseline checks
   - model traceability exports
   - automated regression scoring reports

---

## 17. DevOps, operational readiness, and business maturity conclusion

From repository evidence, this project has:

- Strong engineering fundamentals.
- Active maintenance and release operations.
- Broad analytical capabilities tied directly to practical decisioning operations.

The most important readiness risks are not missing core features but improving:

- secure defaults,
- coverage boundaries,
- and reduction of known technical debt in evolving user interface features.

For teams already operating Pega decisioning at scale, this repository offers immediate practical value and a credible base for internal extension.

---

## 18. Assumptions and unknowns

1. This analysis is static and repository-only; no private infrastructure context is available.
2. No runtime penetration test or dependency vulnerability scanner output was present in repository artifacts.
3. No infrastructure-as-code deployment manifests were found for staging or production runtime.
4. API behavior details are documented from client wrappers and endpoint paths, not from server OpenAPI contracts included in this repository.

