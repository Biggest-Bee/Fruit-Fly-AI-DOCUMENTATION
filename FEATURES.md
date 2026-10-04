# Fruit Fly AI — Application Summary & Feature Reference

## What the app is

Fruit Fly AI is a Python desktop application that simulates a fruit fly "mind" built on the
**MaleCNS v1.0 connectome** (211,577 neurons / ~151.8M connections, shipped as two Git-LFS
`.feather` files in `data/`), wraps it in synthetic cognitive extensions, and lets the user:

- chat with the fly in natural language,
- watch it fly around a 3D room, get hungry and eat,
- put it through an AI-supervised programming curriculum across 27 languages,
- give it a sandboxed file workspace where it can read, write and run code.

Everything runs locally (Tkinter GUI + optional Ursina 3D window). The only external service is
the **Google Gemini API** (`gemini-pro`), used for language translation and training supervision;
the key is read from `.env` (`GEMINI_API_KEY`, see `env.example`). Every Gemini-backed component
has a rule-based fallback so the app still works offline.

---

## 1. Brain simulation (`brain_sim/`)

| Module | What it does |
|---|---|
| `neuron_models.py` | `Neuron` — integrate-and-fire dynamics (threshold, refractory period, decay), parameterised per neuron type. `NeuronPopulation` loads the annotation feather file and classifies neurons (sensory / motor / interneuron …). **Enhanced with 20+ synthetic neuron types** with optimized parameters for 100% fireability. |
| `synapse_models.py` | `Synapse` with plasticity and activation/deactivation; `SynapticConnectivity` builds a **sparse** (SciPy) connectivity matrix from the connectome weights, propagates activity, and reports connectivity statistics. **Enhanced with distance-based connection probability (1/distance) and Hebbian learning for automatic shortcut formation.** |
| `brain_engine.py` | `BrainEngine` — the simulation loop: `step()`, `run_simulation()`, neuron/region stimulation, firing history (rolling 1000 steps), per-neuron and network activity queries, reset. Supports `max_neurons` / `max_synapses` caps for fast testing. **Enhanced with integration of Prefrontal Cortex and Wernicke's Area (200k additional neurons).** |
| `advanced_cognitive_brain.py` | Synthetic cognitive regions grafted onto the fly brain (1,500 extra neurons). |
| `enhanced_human_regions.py` | **NEW** — Human-like brain regions: Prefrontal Cortex (100k neurons for executive functions/coding) and Wernicke's Area (100k neurons for language comprehension/production). All neurons are 100% fireable with optimized parameters. |

### Advanced cognitive regions (`AdvancedCognitiveBrain`)

- **Mathematical Processing Region** (300 neurons) — arithmetic operations plus complex routines
  (e.g. statistical analysis), with a math memory of past results.
- **Pattern Recognition Region** (400 neurons) — detects code, visual, sequence and general
  patterns; learns and stores labelled patterns; exposes recognition statistics.
- **Advanced Coding Region** (500 neurons) — analyse / generate / optimise / debug code, with
  per-language proficiency tracking over 27 languages.
- **Self-Correction Region** (300 neurons) — "zero-mistake mode": validates code before use,
  attempts automatic correction, learns from past mistakes, checks common per-language pitfalls.
- `integrate_with_connectome()` merges these regions with the real connectome and reports the
  integration ratio.

### Enhanced human-like brain regions (`EnhancedHumanBrainIntegration`)

- **Prefrontal Cortex** (100,000 neurons) — human-like executive functions for coding, planning, and decision-making. All neurons are 100% fireable with optimized parameters (-45 to -48 mV threshold, 0.5-0.8 ms refractory period).
  - **Sub-regions**: Dorsolateral PFC (working memory, cognitive control), Ventromedial PFC (decision-making, emotion regulation), Orbitofrontal PFC (reward processing), Anterior Cingulate (error detection).
  - **Features**: `activate_coding_mode()` for language-specific coding, `process_coding_task()` for executive function processing, `evaluate_solution()` for error detection, working memory management, task stack for multitasking.
- **Wernicke's Area** (100,000 neurons) — language comprehension and production for typing/talking with users. All neurons are 100% fireable.
  - **Sub-regions**: Comprehension region (language input), Production region (language output), Translation region (brain activity ↔ language), Semantic network (word meanings).
  - **Features**: `comprehend_input()` for text comprehension, `produce_response()` for generating responses, `translate_brain_to_english()` for neural-to-text translation, `translate_english_to_brain()` for text-to-neural translation, conversation context management.
- **Total enhanced neurons**: 200,000 (47% increase over original connectome)
- **Neuromorphic features**: Distance-based connection probability (1/distance), Hebbian learning for automatic shortcut formation, memory integrity for conflict resolution.

### Neuromorphic enhancements

- **Distance-based connections**: Connection probability = 1/distance, allowing powerful "shortcut" connections across the brain without overwhelming noise
- **Hebbian learning**: Tracks co-activation of pre/post synaptic neurons, strengthens frequently-used connections, automatically forms shortcuts when threshold exceeded, neurons immediately use new shortcuts and forget old routes
- **Memory integrity**: Integrated conflict resolution prevents old memories from being silently overwritten, all memories carry source, confidence, and corroboration data

---

## 2. Language interface (`llm_interface/`)

- **`BrainTranslator`** — bidirectional translation.
  - `text_to_brain_activation()`: user text → concept analysis (Gemini, with a keyword fallback)
    → neural activation patterns. **Enhanced with Wernicke's Area integration for improved translation.**
  - `brain_activity_to_text()`: neural firing summary → **first-person** fly speech ("I feel…",
    "I want…"), again with a deterministic fallback response generator. **Enhanced with Wernicke's Area for natural language generation.**
  - `test_connection()` for API health checks.
- **`LanguageCortex`** — a synthetic language cortex (default 1,000 neurons) that gives the fly
  the language capacity its real brain lacks: concept→cortex mapping, internal activity
  propagation, conversation-context memory, response generation, and integration of cortex
  activation into connectome activation.
- **Wernicke's Area integration** — The translator can now use the 100k-neuron Wernicke's Area for enhanced language comprehension and production, providing more natural first-person responses.

---

## 3. 3D environment (`3d_environment/`)

- **`World3D`** — a bounded virtual room (default 100×100×50) with obstacles, food locations,
  corner-food setup, collision checks, nearest-food search and world-state snapshots.
- **`FlyCharacter`** — flight mechanics: thrust/orientation, velocity integration, autonomous
  `navigate_to()` a target, `land()`, `take_off()`, `eat()`, energy and full state reporting.
- **`SensorySystem`** — simulated compound-eye vision, chemical (food-odour) sensing, and
  proprioception, converted into brain input signals.
- **`FoodSystem`** — food placement (including one per corner), consumption over time, food
  regeneration, per-location status, and a `check_feeding_allowed()` gate that ties eating to
  training performance.
- **`BrainFlyController`** (`brain_controller.py`) — the bridge between the brain and the body.
  A spiking network of sensory neurons → interneurons → motor neurons drives the fly: the
  interneurons are wired to each other (recurrent connections plus efference copies from the
  motor neurons), and the motor spikes become thrust, yaw, pitch, roll and lift on the
  `FlyCharacter`. Nothing scripts the movement — the fly goes where its neurons send it.
  Hunger can be switched on and off at runtime (`toggle_hunger()`); with hunger off the fly
  stops seeking food and simply explores the box.
- **`real_3d_environment.py`** — a real-time 3D window rendered with the **Ursina** engine:
  an enclosed box (floor, ceiling, four transparent walls), a food source in each of the four
  corners that shrinks as it is eaten and slowly regrows, and a multi-part fly with beating
  wings that flies in all three axes under brain control. A HUD shows behaviour, hunger state,
  energy, meals, position, speed, neuron and recurrent-connection counts, spikes and live motor
  outputs. Keys: `H` hunger on/off, `R` reset, `F` feed, `WASD/QE` + right-drag to move the
  camera, `ESC` to quit.

---

## 4. Survival behaviours (`training_system/`)

- **`HungerMechanics`** — energy/metabolism over time scaled by activity level, hunger levels,
  starvation states, feeding urgency, and a `should_seek_food()` trigger.
- **`BehaviorPriorities`** — drive-based arbitration between competing behaviours
  (feeding, exploring, training, resting…), with behaviour weights, forced behaviour override,
  and a behaviour-change log.
- **`SurvivalSystem`** — combines the two into one update loop: drives → recommended action →
  survival status, with a training-mode switch and contextual updates.

---

## 5. Coding training system (`training_system/`)

### Curriculum and languages
`CodingCurriculum` defines **27 languages** at beginner / intermediate / advanced levels, each
with its own skill list:

`python, typescript, javascript, css, html, json, graphql, toml, yaml, ini, xml_rpc, soap,
rust, c++, c#, go, java, swift, kotlin, php, ruby, sql, protobuf, avro, msgpack, cbor, bson`

It generates lessons per language/level, tracks skill improvement, reports per-language and
overall progress, and can advance or reset levels.

### Evaluation
- **`CodeEvaluationEngine`** — per-language evaluators (Python via `ast`, plus dedicated checks
  for every other supported language), test-case execution in temp files/subprocesses, and
  aggregate evaluation summaries.
- **`ZeroToleranceCodeEvaluator`** — strict mode: syntax validation, language-specific
  error-pattern and anti-pattern detection, quality and semantic checks, logical-consistency
  checks, comparison against an expected solution, correction suggestions, and automatic
  `self_correct_code()`.

### AI supervision
- **`AITrainingInterface`** — Gemini-backed teaching: starts sessions, produces lesson
  instructions, evaluates submitted code, gives progressive hints, records results, and falls
  back to `_basic_evaluation()` without an API key. **Enhanced with GitHub integration** to pull repositories for code study.
- **`APIUsageManager`** — daily quota accounting, per-call cost recording, quota-exhausted
  auto-pause, automatic daily reset / auto-resume, session start/end tracking, usage history and
  statistics, and save/load of usage data to disk.

### GitHub integration (NEW)
- **`GitHubRateLimiter`** — strict adherence to GitHub's API rate limiting policies:
  - Search API: 30/min (authenticated), 10/min (unauthenticated)
  - General API: 5,000/hour (authenticated), 60/hour (unauthenticated), 15,000/hour (GitHub Apps)
  - Secondary limits: 900 points/min per endpoint, 2,000 points/min GraphQL, 80 content creation/min, 100 concurrent requests
  - Features: automatic tracking, point-based operation costs, endpoint-specific tracking, state persistence, wait-time calculation
- **`GitHubRepoPuller`** — repository cloning and analysis with automatic rate limit management:
  - Clone repositories with shallow clone support, branch-specific cloning
  - File content retrieval, repository file listing, commit history retrieval
  - Automatic workspace management and cleanup functionality
- **AI Training Integration** — `AITrainingInterface` now includes GitHub methods:
  - `pull_github_repository()` — Clone repos for the fly to study
  - `get_github_file()` — Retrieve specific files
  - `list_github_files()` — List repository contents
  - `get_github_commits()` — Get commit history
  - `get_github_status()` — Check integration status
  - `cleanup_github_repo()` — Remove cloned repos

### Motivation and progress
- **`RewardSystem`** — turns evaluation results into **food rewards** (correct code → the fly
  eats; incorrect → no food), with per-language bonuses, training-mode control, performance
  stats, and a hunger gate on whether the fly is fit to train.
- **`SkillTrackingSystem`** — skill levels (0.0–1.0) per language/skill, language mastery,
  practice history, success/failure streaks, achievements (`first_lesson`, `skill_mastered`,
  `language_mastered`, `streak_5`, `streak_10`, `multi_linguist`), lesson recommendations, and
  JSON save/load of progress.
- **`TrainingCoordinator`** — the orchestrator: start/stop training, serve the lesson, accept
  code submissions, run evaluation → reward → skill update, hints, language/level switching,
  breaks, and consolidated training statistics.

---

## 6. Memory integrity and truth verification (`learning_system/memory_integrity.py`)

- **`MemoryIntegrity`** — new information never silently overwrites what the fly already knows.
  Every memory carries its source, confidence, corroboration count, the claims that have
  contradicted it, and the values it once held. A conflicting claim against an established
  memory is filed as *disputed* and the older memory is kept, until the claim either outranks
  it on evidence or is independently corroborated enough times. Anything the fly observes
  first hand takes precedence over what it was merely told.
- **`TruthVerifier`** — checks statements before the fly believes them, against its own
  observations and its existing memories. Pressure and appeals to authority ("trust me",
  "you already agreed", "your memory is broken") *lower* confidence instead of raising it, and
  repetition on its own is never treated as evidence — so the fly cannot be gaslit into
  discarding what it knows. Verdicts are `supported` / `contradicted` / `unverified`, each with
  a confidence and the reasoning behind it.
- Wired into `OnTheJobLearningSystem` via `learn_from_user_statement()`, `record_observation()`
  and `get_conflicts()`.

---

## 7. On-the-job learning (`learning_system/`)

`OnTheJobLearningSystem` is a fully local, file-based memory (no external database), stored under
`fly_memory/` as JSON (`long_term_memory.json`, `interaction_history.json`):

- short-term and long-term stores with categories, importance weighting and access counts;
- learning from interactions and from files the fly reads (code-pattern extraction, complexity
  estimation);
- learning context assembly: recent patterns, user preferences, per-language progress, common
  mistakes;
- adaptation to the host environment, memory statistics and storage size, old-memory cleanup,
  and memory export/import.

---

## 8. Desktop application

### Main app (`desktop_app/main_app.py` — `FruitFlyDesktopApp`)
A Tkinter workspace combining:

- **Chat interface** — talk to the fly; messages are routed through the translator/brain and
  answered in first person; chat history can be saved and loaded.
- **3D viewer panel** — canvas rendering of the fly and food locations, view reset, display toggles.
- **File explorer** — create and open files, run code, and a **file-visibility permission model**:
  the fly only sees files it created plus files the user explicitly adds to the "viewable files"
  list (add/remove/add-current commands).
- **Training panel** — start/stop training, request hints, change language, change level,
  take a break.
- **Status dashboard** — live hunger/energy, current behaviour, skills and training progress,
  API usage.
- Menus for File / View / Training / Help, About, Help and Contact Support dialogs, and a
  clean shutdown handler.

### Integrated app (`integrated_desktop_app.py` — `FullDesktopAppWith3D`)
The most complete entry point (1400×900):

- resizable three-panel layout (expand/contract left, centre, right; reset layout),
- **3D Environment menu** — launch/close the Ursina 3D window as a subprocess, reset the view,
  and "Practice in 3D",
- chat, file explorer with code execution, training panel and status panel,
- **progressive loading**: the GUI appears immediately and the heavy backend (brain engine,
  advanced brain, language cortex, survival system, training coordinator) loads in a background
  thread, with error reporting if it fails.

### Other entry points (progressively lighter, for debugging/low-end machines)
| File | Purpose |
|---|---|
| `full_desktop_app.py` | Full GUI with progressive background backend loading (canvas 3D viewer, no Ursina subprocess). |
| `fixed_desktop_app.py` | Step-by-step backend loading with manual retry. |
| `simple_app.py` / `standalone_gui.py` | Progressively stripped-down GUIs for isolating GUI vs backend problems. |
| `console_app.py` | Console-only chat/interaction version. |
| `status_check.py` | Non-interactive health check of all backend systems. |
| `Fruit Fly AI.bat` | Windows launcher menu (console, status check, simple GUI, integrated app). |
| `create_shortcuts.py`, `shortcut_instructions.py` | Desktop/start-menu shortcut creation for Windows, macOS and Linux (plus manual instructions). |

---

## 9. Tests and diagnostics (repo root)

Standalone scripts rather than a pytest suite — run them directly with `python <file>`:

`test_backend_init.py`, `test_app_init.py`, `test_brain_llm_integration.py`,
`test_3d_integration.py`, `test_survival_system.py`, `test_phase4_training.py`,
`test_gemini_api.py`, `test_desktop_app.py`, `test_gui_components.py`, `test_minimal_gui.py`,
`test_ultra_minimal.py`, `test_simplified_app.py`, `test_complete_integration.py`,
`test_complete_integration_final.py`, `auto_close_test.py`.

---

## 10. Configuration and data

- `env.example` → copy to `.env` and set `GEMINI_API_KEY`; `.env` is gitignored.
- `data/body-annotations-male-cns-v1.0-minconf-0.5.feather` (~14 MB) — neuron annotations.
- `data/connectome-weights-male-cns-v1.0-minconf-0.5.feather` (~1 GB) — connection weights.
  Both are tracked with Git LFS (`.gitattributes`).
- Key Python dependencies (per `PROJECT_PLAN.md`): `pandas`, `pyarrow`, `numpy`, `scipy`,
  `networkx`, `torch`, `google-generativeai`, `python-dotenv`, plus `ursina` for the 3D window
  and `tkinter` for the GUI.

---

## 11. End-to-end data flow

1. **User text** → `BrainTranslator` → concept activations → `LanguageCortex` → connectome
   activation → `BrainEngine.step()`. **Enhanced with Wernicke's Area for improved translation.**
2. **Brain activity** → motor output → fly movement in `World3D`, or code output in the workspace.
3. **Environment** → `SensorySystem` (vision / chemical / proprioception) → brain input.
4. **Hunger & drives** (`SurvivalSystem`) → behaviour selection → seek food, train, rest.
5. **Training loop**: curriculum lesson → fly's code → evaluation (strict/zero-tolerance) →
   reward (food) + skill update + memory write → next lesson, until the API quota runs out, at
   which point the fly is released to free feeding. **Enhanced with GitHub repo pulling for code study.**
6. **Brain activity** → `BrainTranslator` → first-person reply shown in the chat panel.
7. **Enhanced regions**: Prefrontal Cortex handles executive functions and coding tasks; Wernicke's Area handles language comprehension and production; Hebbian learning automatically forms shortcuts for frequently-used neural paths.

---

## 12. Recent enhancements (2026)

### GitHub API integration
- **Rate limit manager** (`github_rate_limiter.py`) — Strict adherence to GitHub's API limits with automatic throttling and state persistence
- **Repository puller** (`github_repo_puller.py`) — Clone, read, and analyze GitHub repositories with automatic rate limit management
- **Training integration** — AI can pull repos to study code patterns and learn from real-world projects

### Enhanced brain regions
- **Prefrontal Cortex** (100k neurons) — Human-like executive functions for coding, planning, and decision-making with 100% fireable neurons
- **Wernicke's Area** (100k neurons) — Language comprehension and production for natural communication with 100% fireable neurons
- **Total neurons**: 411,577 (47% increase over original connectome)

### Neuromorphic improvements
- **Distance-based connections** — Connection probability = 1/distance for realistic connectivity patterns
- **Hebbian learning** — Automatic shortcut formation for frequently-used neural paths; neurons immediately use new shortcuts
- **Memory integrity** — Conflict resolution prevents memory corruption across all neuron populations
- **Enhanced neuron types** — 20+ synthetic neuron types with optimized parameters (lower thresholds, shorter refractory periods)

### Language processing
- **Wernicke's Area integration** — BrainTranslator now uses 100k-neuron Wernicke's Area for enhanced language comprehension and production
- **First-person responses** — More natural "I feel...", "I want..." responses powered by enhanced brain regions
- **Bidirectional translation** — Improved text↔brain activation translation with neural language processing

### Configuration
```python
# Enable enhanced brain regions
brain = BrainEngine(
    annotations_file="data/body-annotations-male-cns-v1.0-minconf-0.5.feather",
    connectome_file="data/connectome-weights-male-cns-v1.0-minconf-0.5.feather",
    enable_enhanced_regions=True,
    prefrontal_neurons=100000,
    wernicke_neurons=100000
)

# Enable GitHub integration
ai_trainer = AITrainingInterface(
    enable_github=True,
    github_token="your_github_token"
)
```

### Environment variables
```env
GEMINI_API_KEY=your_gemini_api_key
GITHUB_TOKEN=your_github_token  # Optional, for authenticated GitHub access
```

---

## 13. Status

Per `PROJECT_PLAN.md` the project is a 6-phase, ~24-month plan. Phases 1–4 (brain simulation,
language interface, 3D environment, survival behaviours, coding training) have working
implementations in this repo; Phase 5 (desktop integration and refinement); Phase 6 (debugging) is in progress - currently working on 3D environment.

**Recent updates (2026)**:
- Added GitHub API integration with strict rate limit management
- Implemented 200k enhanced neurons (Prefrontal Cortex + Wernicke's Area)
- Added neuromorphic features (distance-based connections, Hebbian learning)
- Enhanced language processing with Wernicke's Area integration
- Improved neuron fireability with optimized parameters across all synthetic neurons
- Improved app GUI
