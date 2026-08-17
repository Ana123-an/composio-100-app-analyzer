# 🤖 100 Apps API & MCP Surface Analyzer

An autonomous multi-agent pipeline built with **Composio SDK** and **Browser-Use** to research, structure, and verify developer surfaces, authentication mechanisms, and Model Context Protocol (MCP) buildability across 100 SaaS and developer platforms.

---

## 🏗️ Architecture & Verification Loop
```mermaid
flowchart TD
    A[100 Apps Seed] --> B[SearchAgent<br><i>Composio Search Tools</i>]
    B --> C[ExtractAgent<br><i>Pydantic Schema Parser</i>]
    C --> D{Confidence Check<br>&ge; 90%?}

    D -- PASS --> E[High Conf Record]
    D -- FAIL --> F[BrowserAgent<br><i>Browser-Use DOM Reader</i>]

    F --> G{Verification Check<br>Passed?}
    G -- PASS --> H[Verified Record]
    G -- FAIL --> I[Human-in-the-Loop]

    E --> J[Final CSV & HTML Data Export]
    H --> J
    I --> J

### Key Design Pillars

1. **Discovery Layer (`SearchAgent`)**: Uses `composio.get_tools(apps=[App.GOOGLE_SEARCH])` to target official API reference pages and developer documentation.
2. **Structured Extraction (`ExtractAgent`)**: Enforces strict typing with Pydantic (`AuthMethod`, `AccessModel`, `APISurface`, `BuildabilityVerdict`).
3. **DOM-Level Verification (`BrowserAgent`)**: Triggers an autonomous headless browser via `browser-use` whenever confidence falls below 90% (e.g., non-indexed docs, complex auth matrices).
4. **Human-in-the-Loop Gate (HitL)**: Automatically tags enterprise sales walls (*PitchBook*, *DealCloud*, *Waterfall.io*) as gated, requiring human verification rather than guessing or hallucinating credentials.

---

## ⚡ Quickstart

### Prerequisites
- Python 3.10+
- Composio API Key (`COMPOSIO_API_KEY`)
- OpenAI API Key (`OPENAI_API_KEY`)

``bash
# 1. Clone the repository
git clone [https://github.com/your-username/composio-100-app-analyzer.git](https://github.com/your-username/composio-100-app-analyzer.git)
cd composio-100-app-analyzer

# 2. Install dependencies
pip install -r requirements.txt

# 3. Authenticate with Composio
composio login

# 4. Run the autonomous pipeline
python run_research.py --input data/research.csv --output data/results.json

├── index.html            # Standalone interactive dashboard & case study
├── README.md             # Pipeline architecture and execution guide
├── run_research.py       # Multi-agent orchestrator powered by Composio & Browser-Use
└── data/
    ├── research.csv      # Complete 100-app input dataset
    └── results.json      # Structured agent execution logs & accuracy metrics
