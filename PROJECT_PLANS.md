# Fruit Fly AI Project Plan

## Project Overview
Building an AI system based on the MaleCNS v1.0 fruit fly connectome that can:
- Communicate with users via natural language
- Navigate a 3D environment
- Learn to code in multiple programming languages
- Function as a desktop application

## Phase 1: Brain Interface Architecture

### 1.1 Language Model "Attachment" System
**Goal**: Create a bidirectional translation interface between human language and fly brain signals

**Components**:
- **Small LLM Interface**: Lightweight language model (~7B parameters) for translation
  - Input: User natural language → Output: Fly brain activation patterns
  - Input: Fly brain activity → Output: Human-readable responses
  - **Translation Training**: The AI translator must be trained to accurately convert brain signals to first-person language
  - **First-Person Perspective**: All translations from the fly's brain are in first-person view ("I think...", "I want...")
- **Brain Signal Translator**: Convert between LLM embeddings and neural activation patterns
- **Brain Extensions**: Since the fly's brain is too small for full conversations, we add synthetic neural extensions
  - **Language Capacity Extension**: Additional neural regions to handle complex language processing
  - **Signal Processing Enhancement**: Extended circuitry to process AI signals and generate appropriate responses
  - **Bidirectional Communication**: Enhanced pathways for AI→brain and brain→AI signal translation
- **Memory Extension**: Extended memory systems for conversation context and long-term communication

**Technical Approach**:
- Use the connectome data to map language concepts to neural pathways
- Create comprehensive "language cortex" extensions for full conversation capacity
- Implement enhanced recurrent connections for conversation context
- Train translator models on fly brain simulation outputs with first-person perspective
- Develop signal processing pipelines for AI-brain communication
- Implement training curriculum for the AI translator to understand fly brain patterns

**Data Requirements**:
- Current: Connectome weights + neuron annotations ✓
- Needed: Neural activation function models, synaptic dynamics
- Needed: AI translator training data and curriculum
- Needed: Brain extension architecture specifications

### 1.2 Brain Simulation Engine
**Goal**: Simulate neural activity in the fly connectome

**Components**:
- **Neuron Models**: Mathematical models for 211,577 neurons
- **Synapse Models**: Dynamic connection strengths based on 151M connections
- **Activation Propagation**: Signal flow through neural network
- **State Management**: Track neural states over time

**Technical Approach**:
- Start with simplified spiking neuron models (Integrate-and-Fire)
- Use connection weights from connectome-weights-male-cns-v1.0-minconf-0.5.feather
- Implement parallel processing for performance
- Optimize for real-time interaction

## Phase 2: 3D Simulation Environment

### 2.1 Virtual World Construction
**Goal**: Create a 3D environment where the fly can navigate

**Components**:
- **3D Rendering Engine**: Unity3D or similar for desktop app
- **Physics System**: Flight mechanics, collision detection
- **Environment Design**: Indoor/outdoor spaces with interactive elements
- **Camera System**: Third-person fly view + user interface

**Features**:
- Flight controls and movement patterns
- Object interaction capabilities
- Spatial awareness using simulated sensory input
- Environmental hazards and rewards

**Technical Approach**:
- Map fly motor neurons to 3D movement controls
- Implement sensory feedback (visual, proprioceptive)
- Create food locations and navigation targets
- Real-time rendering at 60+ FPS

### 2.2 Sensory Input Simulation
**Goal**: Provide the fly brain with simulated sensory data

**Components**:
- **Visual System**: Simulated compound eye input processing
- **Proprioception**: Body position and movement feedback
- **Chemical Sensors**: Food detection, pheromone sensing
- **Touch Sensors**: Surface contact, collision detection

**Technical Approach**:
- Use optic lobe connectome data for visual processing
- Map 3D environment to neural activation patterns
- Implement real-time sensory data streaming to brain simulation

## Phase 3: Survival Behaviors

### 3.1 Hunger and Feeding System
**Goal**: Implement basic survival drives and behaviors

**Components**:
- **Hunger Mechanism**: Metabolic state tracking
- **Food Detection**: Sensory inputs for locating food
- **Navigation System**: Pathfinding to food sources
- **Feeding Behavior**: Landing and eating mechanics

**Implementation**:
- Hunger increases over time, decreases when eating
- Food placed in corners of 3D environment
- Fly uses visual/chemical sensors to locate food
- Automatic navigation when hunger threshold reached
- Eating animation and satisfaction feedback

**Technical Details**:
- Hunger affects neural activity (motivation signals)
- Food locations emit simulated chemical signals
- Pathfinding uses existing motor neuron pathways
- Feeding provides positive reinforcement to neural network

## Phase 4: Coding Training System

### 4.1 Multi-Language Coding Curriculum
**Goal**: Train the fly to code in multiple programming languages

**Target Languages**:
- **Python** (XML versions: lxml, ElementTree)
- **TypeScript** (XML handling: ts-xml-parser)
- **JavaScript** (XML: DOMParser, XMLHttpRequest)
- **CSS** (XML-in-CSS: data-uri, content property)
- **HTML** (XML: XHTML, SVG)
- **JSON** (XML-like: JSON to XML conversion)
- **GraphQL** (XML alternatives: GraphQL over XML)
- **TOML** (XML alternative configuration)
- **4 other format languages** (YAML, INI, XML-RPC, SOAP)

### 4.2 AI Training System
**Goal**: Implement structured training with AI supervision

**Components**:
- **Training AI**: GPT-4 or similar for code generation/evaluation
- **Curriculum System**: Progressive difficulty levels
- **Evaluation Engine**: Automated code testing and feedback
- **Reward System**: Food-based motivation tied to API usage

**Training Process**:
1. **Concept Introduction**: AI explains coding concepts
2. **Code Generation**: Fly attempts to write code
3. **Evaluation**: AI tests and evaluates code quality
4. **Reward System**: 
   - Correct code → Fly gets to eat
   - Incorrect code → No food, continue training
5. **Progress Tracking**: Skill levels per language

**API Usage Management**:
- Training continues until API quota exhausted
- Fly released to free feeding when API depleted
- Training resumes when API usage renewed
- User can stop training at any time

**Technical Implementation**:
- Integration with coding challenge platforms
- Automated test case generation
- Real-time code quality feedback
- Multi-language syntax highlighting and validation

### 4.3 Reinforcement Learning Integration
**Goal**: Use biological motivation for learning

**Components**:
- **Dopamine System**: Simulated reward pathways
- **Hunger-Performance Link**: Motivation affects learning rate
- **Memory Consolidation**: Long-term skill retention
- **Transfer Learning**: Apply coding skills across languages

**Technical Approach**:
- Map successful coding to dopamine release
- Hunger state amplifies reward signals
- Sleep/rest periods for memory consolidation
- Progressive curriculum with increasing complexity

## Phase 5: Desktop Application Integration

### 5.1 User Interface
**Goal**: Create comprehensive desktop application

**Components**:
- **Chat Interface**: Natural language communication
- **3D View Window**: Live fly simulation display
- **File Explorer**: Coding workspace for the fly
- **Control Panel**: Training management, feeding controls
- **Status Dashboard**: Hunger, skills, training progress

**Features**:
- Real-time chat with the fly
- Watch fly navigate 3D environment
- Provide coding tasks and receive solutions
- Monitor training progress and API usage
- Manual feeding and intervention options

### 5.2 File Explorer Integration
**Goal**: Enable fly to work with actual files

**Components**:
- **File System Access**: Safe sandboxed file operations
- **Code Editor**: Fly writes code directly to files
- **Project Management**: Multi-file project support
- **Version Control**: Basic git integration
- **File Visibility System**: Controlled access to files based on ownership and user permissions

**Implementation**:
- Fly can take breaks from coding to eat
- File operations mapped to motor neuron outputs
- Syntax highlighting and error checking
- Project structure understanding
- **File Access Rules**:
  - Fly can only see files it has created or is currently working on
  - User can add files to a "viewable files" section for fly access
  - Default file visibility restricted to fly's own creations
  - User-controlled access permissions for additional files
  - File ownership tracking and permission management

### 5.3 Communication System
**Goal**: Seamless bidirectional communication

**Components**:
- **Speech-to-Text**: User voice input option
- **Text-to-Speech**: Fly verbal responses
- **Emotion Display**: Visual indicators of fly state
- **Context Management**: Conversation history and context

**Technical Approach**:
- Real-time translation between languages
- Personality development based on experiences
- Learning from user interactions
- Adaptive communication style

## Technical Architecture

### System Components
```
┌─────────────────────────────────────────────────────────┐
│                   Desktop Application                    │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │ Chat Interface│  │  3D Viewer   │  │File Explorer │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
└─────────────────────────────────────────────────────────┘
                            │
┌─────────────────────────────────────────────────────────┐
│              Brain Interface & Simulation               │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │ LLM Translator│  │ Brain Engine │  │Sensory Input │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
└─────────────────────────────────────────────────────────┘
                            │
┌─────────────────────────────────────────────────────────┐
│                 Connectome Data Layer                    │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │ 211K Neurons │  │ 151M Connections│ │ Annotations  │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
└─────────────────────────────────────────────────────────┘
```

### Data Flow
1. **User Input** → LLM Translator → Brain Activation Patterns
2. **Brain Activity** → Motor Output → 3D Movement/Code Generation
3. **Sensory Input** → Brain Processing → Decision Making
4. **Brain Output** → LLM Translator → User Response

## Implementation Timeline

### Phase 1: Foundation (Months 1-3)
- [ ] Set up brain simulation environment
- [ ] Implement basic neuron models
- [ ] Create LLM translation interface
- [ ] Test simple language responses

### Phase 2: 3D Environment (Months 4-6)
- [ ] Build 3D simulation world
- [ ] Implement flight mechanics
- [ ] Add sensory input systems
- [ ] Create food and survival mechanics

### Phase 3: Training System (Months 7-12)
- [ ] Develop coding curriculum
- [ ] Integrate AI training system
- [ ] Implement reward mechanisms
- [ ] Add multi-language support

### Phase 4: Application Integration (Months 13-18)
- [ ] Build desktop application UI
- [ ] Integrate file explorer
- [ ] Add communication systems
- [ ] Optimize performance

### Phase 5: Refinement (Months 19-24)
- [ ] Advanced learning algorithms
- [ ] Personality development
- [ ] Performance optimization
- [ ] User testing and feedback

## Technical Challenges & Solutions

### Challenge 1: Brain Scale
**Problem**: 211K neurons, 151M connections is computationally intensive
**Solution**: 
- GPU acceleration for neural simulation
- Optimized sparse matrix operations
- Hierarchical processing for different brain regions

### Challenge 2: Real-time Performance
**Problem**: Need 60+ FPS for 3D while simulating brain
**Solution**:
- Multi-threaded architecture
- Level-of-detail processing
- Predictive caching

### Challenge 3: Language Capacity
**Problem**: Fly brain may lack capacity for complex language
**Solution**:
- Add synthetic language cortex
- Implement external memory systems
- Use compressed representations

### Challenge 4: Training Efficiency
**Problem**: API quota limitations and training time
**Solution**:
- Efficient curriculum design
- Offline training capabilities
- Progressive learning algorithms

## Success Metrics

### Phase 1 Success
- [ ] Fly can respond to simple questions
- [ ] Basic conversation flow established
- [ ] Translation accuracy > 80%

### Phase 2 Success
- [ ] Fly navigates 3D environment smoothly
- [ ] Hunger/feeding system functional
- [ ] Sensory inputs drive behavior

### Phase 3 Success
- [ ] Fly writes functional code in at least 3 languages
- [ ] Training system operates within API limits
- [ ] Skills improve over time

### Phase 4 Success
- [ ] Desktop application runs smoothly
- [ ] File operations work correctly
- [ ] User experience is intuitive

### Phase 5 Success
- [ ] Fly acts as useful coding assistant
- [ ] Personality develops naturally
- [ ] System is stable and performant

## Ethical Considerations

### Animal Welfare (Simulated)
- Ensure "fly" has adequate rest periods
- Prevent overtraining and burnout
- Provide enrichment activities

### AI Safety
- Implement safety guardrails for code generation
- Prevent harmful or malicious code output
- Ensure system doesn't develop harmful behaviors

### User Privacy
- Local processing where possible
- Secure API key management
- Transparent data usage policies

## Configuration and Setup

### API Key Management
**Goal**: Secure configuration of API keys for training AI and other services

**Configuration File**: `.env` file in project root

**Required API Keys**:
```env
# Google Gemini API for training AI
GEMINI_API_KEY=your_gemini_api_key_here

# Additional LLM API keys (if using other services)
OPENAI_API_KEY=your_openai_api_key_here
ANTHROPIC_API_KEY=your_anthropic_api_key_here
COHERE_API_KEY=your_cohere_api_key_here
```

**Security Measures**:
- Never commit `.env` file to version control
- Add `.env` to `.gitignore`
- Use environment variable loading in code
- Implement API key rotation policies
- Monitor API usage and costs

**API Usage Tracking**:
- Real-time quota monitoring
- Cost prediction and alerts
- Automatic training pause when limits reached
- Usage statistics dashboard

### Environment Setup
**Required Software**:
- Python 3.10+ (for brain simulation)
- Unity3D or Godot (for 3D environment)
- Node.js (for desktop application frontend)
- Git (for version control)

**Python Dependencies**:
```
pandas>=2.0.0
pyarrow>=12.0.0
numpy>=1.24.0
torch>=2.0.0
networkx>=3.0
google-generativeai>=0.3.0
python-dotenv>=1.0.0
```

**Project Structure**:
```
fruit-fly-ai/
├── .env                          # API keys (gitignored)
├── .gitignore                   # Git ignore rules
├── README.md                    # Project documentation
├── PROJECT_PLAN.md              # This file
├── data/                        # Connectome data
│   ├── body-annotations-male-cns-v1.0-minconf-0.5.feather
│   └── connectome-weights-male-cns-v1.0-minconf-0.5.feather
├── brain_sim/                   # Brain simulation code
│   ├── neuron_models.py
│   ├── synapse_models.py
│   └── brain_engine.py
├── llm_interface/              # LLM translation code
│   ├── translator.py
│   └── language_cortex.py
├── training_system/            # Coding training system
│   ├── curriculum.py
│   ├── evaluator.py
│   └── reward_system.py
├── desktop_app/                # Desktop application
│   ├── frontend/
│   └── backend/
└── 3d_environment/            # 3D simulation
    ├── unity_project/
    └── assets/
```

## Current Status
Phase 6: Debugging and Testing

### Future Plans
- Continue debugging and testing
- Implement remaining features
- Optimize performance
- Train fly to navigate and interact with the user's device

### Available Data ✓
- MaleCNS v1.0 connectome (211,577 neurons, 151,856,684 connections)
- Neuron annotations and classifications
- Connection weights and synaptic data

### Next Steps
1. Set up project structure and configuration files(done)
2. Configure API keys in `.env` file(done)
3. Set up brain simulation environment(in progress)
4. Implement basic neuron models(in progress)
5. Create LLM integration framework(in progress)
6. Begin 3D environment development(in progress)

---

**Project Start Date**: September 11, 2026
**Estimated Completion**: September 2028
**Current Phase**: Debugging and Testing
**Status**: Foundation Phase - Data Acquisition Complete
