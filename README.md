# SABRE — Synthetic Agent Bio-Swarm Remediation Environment

SABRE is a notebook-driven prototype of a cyber-physical monitoring and response dashboard. It brings several simulated and software-based components together in one Django application: sensor processing, a bio-swarm simulation, document retrieval, and Gemini-powered troubleshooting guidance.


## What it does

- **Sensor fusion:** processes acoustic input and produces spectral information, alongside a synthetic thermal grid and hotspot information. Librosa is used when available; a NumPy fallback is included.
- **Bio-swarm simulation:** models agents moving across a bounded grid toward a selected fault zone. The simulation is software-based and does not control physical devices.
- **Manual-grounded retrieval:** indexes PDF documents and retrieves related passages for a troubleshooting query. The notebook includes clearly marked demonstration seed material; demo content should not be treated as verified OEM guidance.
- **Gemini remediation:** uses retrieved context to produce a structured diagnostic response and suggested corrective steps. It is intended as a decision-support demonstration, not a substitute for validated procedures or a qualified operator.
- **Dashboard and API:** Django serves the dashboard and JSON endpoints. The front end uses local JavaScript and canvas-based visualizations rather than third-party script libraries.


## Architecture

The notebook writes the project into a `Cyber/` directory. The generated application is organized into:


| Component | Responsibility |
| --- | --- |
| `core_project/` | Django configuration, routing, middleware, WSGI and ASGI entry points |
| `dashboard_app/` | Views, API routes, access checks and request validation |
| `modules/sensor_fusion.py` | Acoustic processing, thermal simulation and fusion results |
| `modules/swarm_engine.py` | Bio-swarm movement and target-zone simulation |
| `modules/vector_rag.py` | PDF ingestion, chunking, embeddings and similarity search |
| `modules/llm_engine.py` | Gemini response generation with retrieved context |
| `templates/`, `static/` | Dashboard pages, styles and browser-side logic |
| `tests/` | Unit, API, engine, fallback, security and stress checks |


## Running it

The notebook is the intended entry point, particularly in Google Colab.


1. Open `SABRE.ipynb` in Colab or a Jupyter environment.
2. Run the environment/setup cell first. It installs available dependencies using binary wheels and reads configuration.
3. Run the remaining notebook cells in order. They create the `Cyber/` project, its files, and run checks.
4. Follow the final notebook cell's instructions to start and access the dashboard. If using a tunnel, configure it for your environment.


## Configuration

The notebook can read configuration from environment variables and `.env` files. The Gemini key is obtained from the environment, dotenv configuration, Colab Secrets, or a hidden prompt, depending on the notebook environment. Keep API credentials private and do not commit `.env` files.


The generated `Cyber/.env.example` documents configuration options, including:

- `GEMINI_API_KEY` and optional model selection
- dashboard access token and trusted origins
- demo-mode behavior and request rate limits
- HTTPS and proxy settings
- vector-store location and RAG embedder/store selection

Review the generated `.env.example` before exposing the dashboard outside your local environment. Set trusted origins, transport security, and access controls appropriately for the hosting setup.


## Dependencies and fallbacks

Django and the core numerical stack are used by the application. Optional packages support stronger embeddings, Chroma storage, and audio processing. The notebook attempts to use available implementations and can fall back to lighter alternatives, including ONNX or hashing-based embeddings and NumPy-backed storage. These fallbacks keep the demo usable in constrained notebook environments, but retrieval quality can vary.


## Scope and limitations

SABRE is a simulation and prototype dashboard. Sensor values and simulated trajectories are not measurements from real equipment unless real inputs are explicitly supplied. AI-generated recommendations may be incorrect; verify them against approved documentation and operating procedures before acting. Optional packages may be skipped when installation is unavailable, which can change the capabilities or quality of a subsystem.
