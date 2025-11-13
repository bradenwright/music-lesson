# Music Lessons Project Roadmap

## Project Vision

Build a comprehensive system for tracking bass lessons, organizing music theory knowledge, and automating the processing of lesson content through AI agents. The system will evolve from manual documentation to a fully automated pipeline with specialized AI agents handling different aspects of lesson processing.

## Current Phase: Foundation & Manual Processing

### Goals
- Establish solid understanding of requirements and workflows
- Build out comprehensive documentation structure
- Create and refine AI prompt instructions
- Manually process lessons to validate approach
- Identify pain points and automation opportunities

### Status: In Progress

### Tasks
- [x] Create project structure (lesson-summary, lesson-library, lesson-plans, songs)
- [x] Build comprehensive README and documentation
- [x] Create AI prompt instructions document
- [x] Process initial lessons manually
- [ ] Continue refining AI prompt instructions based on experience
- [ ] Process multiple lessons to identify patterns and edge cases
- [ ] Document common issues and solutions

### Deliverables
- Complete documentation structure
- Refined AI prompt instructions
- Validated workflow for manual processing
- Clear understanding of automation needs

---

## Phase 2: File Management & Upload

### Goals
Make it easier to get lesson files (transcripts, recordings, images) into the system for AI processing. Also enable lesson plan generation through AI prompts.

### Current Workflow (Phase 2A)

**Status**: In use now

**Process**:
1. Teacher (Paul) emails lesson files to user (Braden)
   - Transcripts
   - Audio/video recordings
   - Notation images
   - GuitarPro files
2. User downloads files manually
3. User organizes and processes files with AI prompt

**Benefits**:
- ✅ Simple, works immediately
- ✅ No infrastructure needed
- ✅ Teacher just needs to email
- ✅ User has full control

**Limitations**:
- ❌ Manual download required
- ❌ Manual file organization
- ❌ Not scalable for multiple students

### Future Workflow (Phase 2B - Phase 3 or later)

**Goal**: Simplify file upload for teacher, automate processing

**Solution**: Simple web frontend + GCS integration

**Architecture**:
```
[Teacher] → [Web Frontend] → [GCS Upload] → [GCS Bucket]
                                              ↓
[App] ← [Process from GCS] ← [GCS Bucket]
```

**Features**:
- Simple web interface for teacher
- Upload transcript files
- Upload audio/video recordings
- Upload notation images
- Upload GuitarPro files
- Specify lesson date/student
- Files automatically uploaded to GCS (Google Cloud Storage)
- App processes files directly from GCS
- No manual download needed

**Benefits**:
- ✅ Teacher-friendly (just upload via web)
- ✅ Automated file handling
- ✅ Files stored in cloud (GCS)
- ✅ App can process directly from GCS
- ✅ Scalable for multiple students

**Timeline**: Phase 3 or after (when automation pipeline is ready)

**Technical Considerations**:
- Web frontend (simple React/Next.js)
- GCS bucket for file storage
- App integration to read from GCS
- File organization in GCS (by student, date, etc.)
- Security/authentication for teacher access

### Deliverables

**Phase 2A (Current)**:
- ✅ Manual email/download workflow
- ✅ File organization process

**Phase 2B (Future)**:
- [ ] Simple web frontend for teacher
- [ ] GCS integration
- [ ] App processing from GCS
- [ ] File organization in GCS
- [ ] Teacher authentication/access

### Lesson Plan Generation (Phase 2.5)

**Initial Approach: AI Prompt Interface**
- Web interface with AI prompt to help generate lesson plan files
- Input form for lesson plan details (topic, duration, objectives, songs, etc.)
- AI generates structured lesson plan markdown in correct format
- Can download or save directly to repo structure
- Use case: Instructor describes what they want to teach, AI generates structured lesson plan

**Future Integration (Stage 4: Teacher Global Library)**
- Enhanced web interface for instructor
- Pulls from global catalog/library when creating lesson plans
- Access to all existing lesson plans as starting points/templates
- Access to global song library with reusable charts and GP files
- Smart suggestions based on:
  - Previous lesson plans
  - Student progress and history
  - Available songs with charts/GP files
  - Knowledge base entries
- Reuse existing content:
  - Select songs that already have charts/GP files
  - Reference existing lesson plans as templates
  - Pull from knowledge base for theory concepts
  - Maintain consistency across students

---

## Phase 3: AI Automation Pipeline

### Vision: Specialized AI Agents

Rather than one monolithic AI system, use multiple specialized agents that each excel at specific tasks:

1. **lesson-plan-agent**
   - **Purpose**: Interactive prompt for teacher and student to use during live calls
   - **Function**: Generates lesson plan (.md file) that can be refined
   - **Use Case**: Teacher and student collaborate in real-time to create structured lesson plans
   - **Output**: Creates/updates lesson plan markdown files in `lesson-plans/`
   - **Features**: 
     - Interactive conversation during lesson planning
     - Real-time refinement and editing
     - Structured lesson plan format
     - Can reference existing lesson plans and templates

2. **lesson-summary-agent**
   - **Purpose**: Process lesson transcripts and uploaded files to create lesson summaries
   - **Function**: 
     - Takes transcript and various uploaded files
     - Creates content in `lesson-summary/` folder
     - Organizes uploaded files appropriately
     - Adds links to relevant areas (lesson plans, songs, library entries)
   - **Use Case**: After a lesson, process transcript and files to generate summary
   - **Output**: 
     - Lesson summary markdown file (YYYY-MM-DD.md)
     - Organized file structure
     - Links to lesson plans, songs, library entries
   - **Features**:
     - Extracts key topics, assignments, next steps
     - Links to relevant lesson plans
     - Links to songs covered
     - Links to knowledge extracted to library

3. **lesson-library-agent**
   - **Purpose**: Generate permanent, organized information in the lesson library
   - **Function**: 
     - Identifies reusable concepts from lessons
     - Categorizes knowledge appropriately (scales-modes, harmony-theory, techniques, etc.)
     - Creates/updates library entries
     - Maintains cross-references
   - **Use Case**: Extract lasting knowledge from lessons for future reference
   - **Output**: Creates/updates markdown files in `lesson-library/` organized by topic
   - **Features**:
     - More organized and permanent than lesson summaries
     - Searchable knowledge base
     - Cross-references between concepts
     - Links back to source lessons
   - **Future Evolution (TBD)**:
     - May call specialized topic agents (e.g., scales-agent, music-theory-agent)
     - Or may delegate to separate agents for each topic area
     - Architecture decision: orchestrator pattern vs. specialized agents
     - Will be determined based on complexity and needs

4. **lesson-song-agent** (May be part of lesson-summary-agent)
   - **Purpose**: Create and manage song entries with context and files
   - **Function**:
     - Creates song folders in `songs/`
     - Adds context: BPM, key, version, artist, etc.
     - Organizes files: GP files, images (notation screenshots/photos)
     - Links songs to lessons and lesson plans
   - **Use Case**: When songs are covered in lessons, create/update song entries
   - **Output**: 
     - Song folder structure
     - Song README.md with metadata
     - Organized GP files and images
     - Links to lessons where covered
   - **Features**:
     - Extracts song information from lessons
     - Handles version information (e.g., Grateful Dead version, Hot Rize version)
     - Manages file organization (images/, guitarpro/ folders)
   - **Note**: May be integrated into lesson-summary-agent, or separate for specialized song processing

### Agent Responsibilities Summary

**lesson-plan-agent**:
- Interactive prompt for live lesson planning sessions
- Teacher and student collaborate in real-time
- Generates structured lesson plan markdown files
- Can reference existing plans and templates

**lesson-summary-agent**:
- Primary processor for lesson transcripts and files
- Creates lesson summary markdown files
- Organizes uploaded files (transcripts, recordings, images)
- Adds links to lesson plans, songs, and library entries
- May include song processing functionality (or delegates to lesson-song-agent)

**lesson-library-agent**:
- Extracts permanent, reusable knowledge from lessons
- Organizes by topic (scales-modes, harmony-theory, techniques, etc.)
- Creates searchable knowledge base entries
- Maintains cross-references between concepts
- **Future (TBD)**: May call specialized topic agents or delegate to separate agents
  - Potential specialized agents: scales-agent, music-theory-agent, techniques-agent, etc.
  - Architecture decision pending based on complexity and needs

**lesson-song-agent**:
- Specialized song processing (may be part of lesson-summary-agent)
- Creates song folder structure
- Extracts metadata (BPM, key, version, artist)
- Organizes GP files and images
- Links songs to lessons and lesson plans

**Decision Point**: Whether lesson-song-agent is separate or integrated into lesson-summary-agent depends on:
- Complexity of song processing requirements
- Whether song processing needs specialized logic
- Whether it's simpler to handle songs as part of summary processing
- Can start integrated, extract later if needed

### Architecture Options

#### Option 1: n8n Pipeline
- **Description**: Use n8n for workflow orchestration
- **Pros**: Visual workflow builder, good integrations, active development
- **Cons**: Requires n8n setup and maintenance

#### Option 2: Custom AI Agent System
- **Description**: Build custom system with specialized agents
- **Communication**: NATS (message bus)
  - Experience: Used locally with Docker and in GKE
  - Benefits: Lightweight, scalable, good for microservices
- **Pros**: Full control, optimized for specific needs
- **Cons**: More development effort

#### Option 3: Kubernetes-based Agents
- **Description**: Deploy agents as K8s services
- **Communication**: NATS in cluster
- **Pros**: Scalable, production-ready, good for cloud deployment
- **Cons**: Requires K8s infrastructure
- **Note**: There was a webinar on AI agents in K8s (worth reviewing)

#### Option 4: Hybrid Approach
- **Description**: Start with n8n for orchestration, use NATS for agent communication
- **Pros**: Best of both worlds
- **Cons**: More complex architecture

### Recommended Approach

**Phase 3A: Manual Processing (Current)**
- **Status**: In use now
- **Process**: Manually copy/paste AI_PROMPT_INSTRUCTIONS.md into each prompt
- **Purpose**: Validate workflow, refine instructions, process lessons
- **Next**: Move to agent framework when ready

**Phase 3B: Agent Framework Integration**
- **Process**: Use existing agent framework
- **Architecture**:
  ```
  [Agent Framework]
      ↓ (sends request)
  [cursor-agent] (requires Cursor IDE running locally)
      ↓ (processes with ai-instructions + commands)
  [File Operations]
      ↓ (sends ack)
  [Agent Framework]
  ```
- **Key Details**:
  - Agent has `ai-instructions` section (contains AI_PROMPT_INSTRUCTIONS.md content)
  - Agent has `command` section (file operations, git, etc.)
  - cursor-agent processes and executes
  - Returns acknowledgment when complete
- **Benefits**:
  - Automated processing
  - No manual copy/paste needed
  - AI_PROMPT_INSTRUCTIONS.md embedded in agent config
  - Leverages existing infrastructure
- **Limitation**: Requires Cursor IDE running locally

**Phase 3C: LLM/MCP Server Replacement**
- **Goal**: Remove dependency on Cursor IDE
- **Options**:
  - **Direct LLM API**: Replace cursor-agent with direct OpenAI/Anthropic calls
  - **MCP Server**: Use Model Context Protocol server for LLM access
  - **Local LLM**: Run models locally (Ollama, vLLM, etc.)
- **Architecture**:
  ```
  [Agent Framework]
      ↓ (sends request)
  [LLM/MCP Server] → [OpenAI/Anthropic/Local LLM]
      ↓ (processes with instructions)
  [File Operations via Agent]
      ↓ (sends ack)
  [Agent Framework]
  ```
- **Benefits**:
  - No Cursor IDE dependency
  - Can deploy independently
  - Flexible LLM provider choices
  - Can run in Docker Compose or GKE

**Phase 3D: NATS-Based Microservices (Future)**
- **Architecture**: Full microservices with NATS (see detailed section below)
- **Deployment**: Docker Compose locally, GKE for production
- **When**: If need to scale or want specialized agents

---

## AI Agent Implementation Details

### Architecture Options

#### Option A: NATS-Based Microservices (Recommended)
**Description**: Each agent is a separate microservice communicating via NATS

**Architecture**:
```
[Orchestrator/API Gateway]
    ↓
[NATS Message Bus]
    ↓
┌─────────────────────────────────────┐
│  [lesson-plan-agent]                 │
│  [lesson-summary-agent]              │
│  [lesson-library-agent]              │
│  [lesson-song-agent]                 │
└─────────────────────────────────────┘
```

**Communication Pattern**:
- **NATS Subjects**: Each agent subscribes to specific subjects
  - `lesson.plan.create` - Lesson plan creation requests
  - `lesson.summary.process` - Lesson summary processing requests
  - `lesson.library.extract` - Knowledge extraction to library requests
  - `lesson.song.process` - Song processing requests
- **Request/Reply Pattern**: Orchestrator sends request, agent replies with result
- **Pub/Sub Pattern**: For notifications and status updates

**Benefits**:
- ✅ NATS experience already exists (Docker and GKE)
- ✅ Lightweight and fast
- ✅ Good for microservices architecture
- ✅ Easy to add/remove agents
- ✅ Works well in both local and cloud environments

#### Option B: n8n Workflow Orchestration
**Description**: Use n8n for visual workflow building, agents as nodes

**Architecture**:
- n8n workflows define the pipeline
- Each agent can be a custom n8n node or external service
- Can integrate with NATS for agent communication

**Benefits**:
- Visual workflow builder
- Good for non-technical users
- Many integrations available

**Considerations**:
- May be overkill for specialized agents
- Less flexible than pure microservices

#### Option C: Hybrid: n8n + NATS Agents
**Description**: n8n for orchestration, NATS for agent-to-agent communication

**Architecture**:
- n8n handles initial workflow and file upload
- NATS handles agent communication and coordination
- Best of both worlds

### Deployment Options

#### Local Development: Docker Compose

**Structure**:
```yaml
services:
  nats:
    image: nats:latest
    ports:
      - "4222:4222"
  
  orchestrator:
    build: ./orchestrator
    depends_on:
      - nats
    environment:
      - NATS_URL=nats://nats:4222
  
  lesson-plan-agent:
    build: ./agents/lesson-plan
    depends_on:
      - nats
    environment:
      - NATS_URL=nats://nats:4222
      - OPENAI_API_KEY=${OPENAI_API_KEY}
  
  lesson-summary-agent:
    build: ./agents/lesson-summary
    depends_on:
      - nats
    environment:
      - NATS_URL=nats://nats:4222
      - OPENAI_API_KEY=${OPENAI_API_KEY}
  
  lesson-library-agent:
    build: ./agents/lesson-library
    depends_on:
      - nats
    environment:
      - NATS_URL=nats://nats:4222
      - OPENAI_API_KEY=${OPENAI_API_KEY}
  
  lesson-song-agent:
    build: ./agents/lesson-song
    depends_on:
      - nats
    environment:
      - NATS_URL=nats://nats:4222
      - OPENAI_API_KEY=${OPENAI_API_KEY}
    # Note: May be integrated into lesson-summary-agent instead
```

**Benefits**:
- ✅ Easy local development
- ✅ Matches production architecture
- ✅ Can test full pipeline locally
- ✅ Fast iteration cycle

#### Production: Google Kubernetes Engine (GKE)

**Structure**:
- Each agent as a Kubernetes Deployment
- NATS as a StatefulSet or managed service
- ConfigMaps for configuration
- Secrets for API keys
- Service mesh (optional) for advanced routing

**Deployment Strategy**:
- **Development**: Docker Compose locally
- **Staging**: GKE cluster (small, for testing)
- **Production**: GKE cluster (scaled, high availability)

**Benefits**:
- ✅ Scalable and production-ready
- ✅ Can scale agents independently
- ✅ High availability
- ✅ Easy to add new agents
- ✅ Matches existing GKE experience

### Agent Implementation Approaches

#### Approach 1: LLM API Wrappers (Recommended Start)
**Description**: Agents are wrappers around LLM APIs (OpenAI, Anthropic, etc.)

**How it works**:
- Each agent has specialized prompts
- Agent receives task via NATS
- Calls LLM API with context and prompt
- Processes response and sends result back

**Pros**:
- ✅ Fast to implement
- ✅ No training required initially
- ✅ Easy to iterate on prompts
- ✅ Can switch LLM providers easily

**Cons**:
- ❌ API costs per request
- ❌ Latency depends on API
- ❌ Less control over model behavior

#### Approach 2: Local LLM Models
**Description**: Run open-source LLMs locally (Llama, Mistral, etc.)

**How it works**:
- Deploy LLM models in containers
- Agents call local model endpoints
- No external API dependencies

**Pros**:
- ✅ No API costs
- ✅ Data privacy (stays local)
- ✅ No rate limits
- ✅ Full control

**Cons**:
- ❌ Requires GPU resources
- ❌ More complex setup
- ❌ May need model optimization
- ❌ Higher infrastructure costs

#### Approach 3: Hybrid (Recommended Long-term)
**Description**: Use API for development, local models for production

**Benefits**:
- Start with APIs for speed
- Move to local models when needed
- Best of both worlds

### Training & Refining Agents/LLMs

#### Level 1: Prompt Engineering (Start Here)
**What it is**: Crafting effective prompts to get desired outputs

**Techniques**:
- **Few-shot learning**: Provide examples in prompt
- **Chain of thought**: Ask model to think step-by-step
- **Role-based prompts**: "You are an expert music teacher..."
- **Structured outputs**: Request specific formats (JSON, markdown)
- **Context injection**: Include relevant files/content in prompt

**For this project**:
- Use AI_PROMPT_INSTRUCTIONS.md as base prompt
- Add examples of good outputs
- Include context from lesson plans, library, etc.
- Refine based on actual outputs

**Tools**:
- Prompt testing frameworks
- A/B testing different prompts
- Output validation scripts

#### Level 2: Retrieval-Augmented Generation (RAG)
**What it is**: Enhance prompts with relevant context from knowledge base

**How it works**:
1. Agent receives task
2. Searches lesson-library, lesson-plans, songs for relevant context
3. Includes relevant context in prompt
4. LLM generates response with better context

**For this project**:
- lesson-summary-agent: Pull previous lesson summaries, lesson plan context
- lesson-library-agent: Check existing library entries to avoid duplicates
- lesson-song-agent: Check existing song entries for consistency
- lesson-plan-agent: Reference existing lesson plans and templates

**Implementation**:
- Vector database (Pinecone, Weaviate, or local Chroma)
- Embedding models (OpenAI, local)
- Semantic search over markdown files

#### Level 3: Fine-Tuning
**What it is**: Train model on specific data to improve performance

**When to use**:
- When prompt engineering isn't enough
- Need consistent formatting
- Domain-specific knowledge required
- Want to reduce API costs

**Process**:
1. Collect training data (good examples of desired outputs)
2. Format as training examples
3. Fine-tune base model
4. Deploy fine-tuned model

**For this project**:
- Could fine-tune on lesson summaries
- Train on knowledge extraction examples
- Customize for music education domain

**Considerations**:
- Requires training data (need many examples)
- Training costs
- Model hosting
- May need to retrain as data grows

#### Level 4: Custom Training (Advanced)
**What it is**: Train models from scratch or heavily modify

**When to use**:
- Very specific domain requirements
- Need complete control
- Have large dataset
- Want to optimize for specific tasks

**For this project**:
- Probably overkill initially
- Consider if system grows significantly

### Recommended Learning Path

**Phase 1: Prompt Engineering (Now)**
- Start with well-crafted prompts
- Use AI_PROMPT_INSTRUCTIONS.md
- Iterate based on results
- Build up examples and patterns

**Phase 2: RAG Integration (After Phase 3A)**
- Add semantic search to agents
- Enhance prompts with relevant context
- Improve accuracy and consistency

**Phase 3: Fine-Tuning (If Needed)**
- If prompt engineering + RAG isn't sufficient
- Collect training data from good outputs
- Fine-tune for specific tasks

**Phase 4: Local Models (If Needed)**
- If API costs become too high
- If privacy becomes critical
- If need more control

### Implementation Recommendations

**Phase 3A: Manual (Current)**
1. Copy/paste AI_PROMPT_INSTRUCTIONS.md into each prompt
2. Process lessons manually
3. Refine instructions based on results
4. Validate workflow

**Phase 3B: Agent Framework**
1. Create agent in existing framework
2. Embed AI_PROMPT_INSTRUCTIONS.md in agent's ai-instructions section
3. Configure commands for file operations
4. Test with cursor-agent (Cursor IDE running)
5. Process lessons automatically
6. Refine agent configuration

**Phase 3C: LLM/MCP Replacement**
1. Set up LLM API or MCP server
2. Replace cursor-agent call with new LLM endpoint
3. Test with same agent framework
4. Remove Cursor IDE dependency
5. Deploy independently (Docker Compose or GKE)

**Phase 3D: NATS Microservices (Future)**
1. Build specialized agents as microservices
2. Use NATS for communication
3. Deploy locally with Docker Compose
4. Scale to GKE when needed
5. Add RAG for context enhancement
6. Consider fine-tuning if needed

### Tools & Technologies

**NATS**:
- Official NATS Docker images
- NATS clients (Go, Python, Node.js, etc.)
- NATS JetStream for persistence (if needed)

**LLM APIs**:
- OpenAI (GPT-4, GPT-3.5)
- Anthropic (Claude)
- Google (Gemini)
- Local: Ollama, vLLM, etc.

**Vector Databases** (for RAG):
- Pinecone (managed)
- Weaviate (self-hosted or managed)
- Chroma (local, simple)
- Qdrant (self-hosted)

**Development**:
- Docker Compose for local
- Kubernetes for production
- Python or Node.js for agents (both have good NATS and LLM libraries)

**Agent Framework** (Phase 3B):
- Existing agent framework (already built)
- cursor-agent integration (requires Cursor IDE)
- ai-instructions and command sections
- Request/acknowledgment pattern

**MCP (Model Context Protocol)** (Phase 3C):
- Standardized LLM access
- Tool/context management
- Works with OpenAI, Anthropic, local models
- Can replace cursor-agent dependency

### Agent Communication Pattern

```
[File Upload] 
    ↓
[Orchestrator] (n8n or custom)
    ↓
[NATS Message Bus]
    ↓
┌─────────────────────────────────────┐
│  [lesson-plan-agent]                 │
│  [lesson-summary-agent]              │
│  [lesson-library-agent]              │
│    └─→ [scales-agent] (TBD)          │
│    └─→ [music-theory-agent] (TBD)   │
│    └─→ [techniques-agent] (TBD)      │
│  [lesson-song-agent]                 │
└─────────────────────────────────────┘
    ↓
[File System / Git Repo]

Note: Specialized topic agents (scales, music-theory, etc.) are TBD
- May be called by lesson-library-agent
- Or may be separate agents that lesson-library-agent delegates to
- Architecture decision pending
```

### Deliverables
- Working AI agent pipeline
- Specialized agents for each task
- Automated lesson processing
- Integration with existing repo structure

---

## Phase 4: Advanced Features

### Potential Enhancements
- **Search functionality**: Full-text search across all lessons, library, and songs
- **Audio/video analysis**: Extract techniques from recordings (see Phase 5 for details)
- **Practice tracking**: Integration with practice logs
- **Progress visualization**: Charts and graphs of learning progress
- **Automated transcription**: Direct from Zoom/recordings
- **Git integration**: Automated commits and PRs for lesson updates
- **Multi-user support**: Student isolation and instructor management

### Timeline: TBD
- Prioritize based on Phase 3 learnings and actual usage

---

## Phase 5: Audio/Video Recording & Analysis (Future Vision)

### Current State
- **Primary Input**: Transcripts for lesson processing
- **Recording**: Manual transcription from recordings (Zoom, etc.)
- **Analysis**: Text-based analysis from transcripts

### Future Vision: Rich Media Integration

**Recording Tool: farplay.io**
- **Why farplay.io**: 
  - Paid version provides video recording
  - **Separate audio tracks** for each participant
  - **Speaker identification** - can tell who's talking
  - **Separate bass audio track** - isolate instrument audio
  - **Video recording** - capture technique visually

**Key Advantages**:
- Multi-track audio enables detailed analysis
- Video provides visual technique feedback
- Speaker separation improves transcription accuracy
- Isolated instrument tracks for musical analysis

### Potential Use Cases

#### 1. Audio Alignment Analysis
- **Compare student's bass playing with GuitarPro files**
  - Analyze how well student plays along with backing tracks
  - Measure timing accuracy and rhythm alignment
  - Identify areas where student is ahead/behind the beat
  - Visualize alignment between student performance and reference

#### 2. Technique Analysis from Video
- **Visual technique review**
  - Analyze hand positioning and finger placement
  - Review posture and instrument positioning
  - Identify technique issues or improvements
  - Compare technique across lessons to track progress
  - Frame-by-frame analysis of specific techniques
  - Side-by-side comparison with reference videos

#### 3. Multi-Track Audio Analysis
- **Separate audio tracks enable**:
  - Isolating bass audio for detailed frequency analysis
  - Comparing instructor's playing with student's
  - Analyzing timing and rhythm separately
  - Tone quality assessment
  - Dynamic range and expression analysis

#### 4. Enhanced Transcription
- **Better transcription quality**:
  - Use separate audio tracks for improved accuracy
  - Speaker identification (instructor vs. student)
  - Better handling of overlapping speech
  - Music detection and separation from speech
  - Automatic timestamping of key moments

#### 5. Progress Tracking & Metrics
- **Quantifiable progress**:
  - Visual comparison of technique over time
  - Audio quality improvements tracking
  - Rhythm and timing accuracy metrics
  - Practice effectiveness measurement
  - Automated progress reports

#### 6. Interactive Ear Training Sessions (Gamified)
- **Training Mode**: 
  - Tones/notes are played, student tries to mimic on bass
  - Real-time feedback on accuracy
  - System analyzes if student played correct note/pitch
  
- **Gamification Elements**:
  - Score/points for accuracy
  - Progress tracking and streaks
  - Difficulty levels (beginner to advanced)
  - Achievement system and badges
  - Leaderboards (optional, for motivation)
  
- **Multiple Reference Types** (can be toggled/changed):
  - **Notation**: Standard music notation display
  - **Color per Note**: Visual color coding for each note (helps visual learners)
  - **Tab**: Tablature display (familiar format)
  - **No Visual**: Audio only (pure ear training, most challenging)
  - **Combination**: Mix of references (e.g., color + notation)
  
- **Adaptive Learning**:
  - System can change which reference is shown
  - Gradually reduce visual aids as ear improves
  - Customize difficulty based on student progress
  - Focus on weak areas identified from previous sessions
  
- **Training Scenarios**:
  - **Pitch Recognition**: Single notes, identify and play back
  - **Interval Training**: Play intervals, identify by ear
  - **Scale Recognition**: Play scales, identify which scale
  - **Chord Tone Identification**: Identify notes within chords
  - **Root Note Identification**: Building on existing ear training concepts
  - **Melodic Dictation**: Play back short melodies
  
- **Integration with Existing System**:
  - Links to ear training concepts in lesson-library
  - Tracks progress in student's lesson history
  - Can be assigned as practice homework
  - Results feed into lesson summaries and progress tracking

### Technical Considerations

**Integration**:
- farplay.io API integration or file export
- Storage of video and multi-track audio files
- Processing pipeline for audio/video analysis

**Analysis Tools**:
- AI models for technique analysis (computer vision)
- Audio alignment algorithms
- Speech-to-text with speaker identification
- Music information retrieval (MIR) for audio analysis
- Frequency and waveform analysis
- **Ear Training System**:
  - Real-time pitch detection and note recognition
  - Audio comparison algorithms (reference vs. student)
  - Visual rendering engine (notation, colors, tabs)
  - Gamification engine (scoring, achievements, progress)
  - Adaptive difficulty algorithms
  - Integration with lesson library and progress tracking

**Infrastructure**:
- Large file storage (video files are large)
- Processing power for video/audio analysis
- Efficient encoding and compression
- Privacy and data management for video content

**Challenges**:
- Large file sizes for video content
- Processing power requirements
- Privacy considerations with video recordings
- Cost of storage and processing
- Determining most valuable use cases before building
- Integration complexity

### Implementation Approach

**Phase 5A: Recording Integration**
- Integrate farplay.io recording
- Store video and multi-track audio files
- Basic playback and review interface

**Phase 5B: Basic Analysis**
- Start with one use case (e.g., audio alignment or technique review)
- Build analysis tools for that specific use case
- Validate value before expanding

**Phase 5C: Advanced Analysis**
- Expand to additional use cases
- Build comprehensive analysis suite
- Integrate insights into lesson summaries and progress tracking

**Phase 5D: Interactive Ear Training (Gamified)**
- Build interactive ear training system
- Real-time audio analysis and feedback
- Multiple visual reference modes (notation, color, tab)
- Gamification elements (scoring, achievements, progress)
- Adaptive difficulty system
- Integration with existing ear training concepts
- Link to lesson assignments and progress tracking

### Success Criteria
- Seamless recording integration with farplay.io
- Valuable insights from audio/video analysis
- Actionable feedback for student improvement
- Efficient storage and processing
- Clear use cases validated and prioritized
- Improved learning outcomes from rich media analysis
- **Ear Training**: Engaging, effective gamified training sessions
- **Ear Training**: Measurable improvement in pitch recognition and ear skills
- **Ear Training**: Flexible reference modes support different learning styles

### Notes
- This is a long-term vision - focus on core system first
- Video and multi-track audio provide rich data for future analysis
- Use cases should be validated before heavy investment
- Start simple, expand based on actual value demonstrated
- **Ear Training**: Gamification makes practice more engaging and measurable
- **Ear Training**: Multiple reference types allow gradual progression from visual to pure ear
- **Ear Training**: Builds on existing ear training concepts in lesson-library

---

## Rollout Strategy

### Stage 1: Single User (Current)
**Status**: In Progress

**Scope**:
- Project owner (Braden) uses system for personal lessons
- Manual processing and refinement
- Validate all workflows and features

**Goals**:
- System works reliably for single user
- All workflows validated
- Documentation complete
- Ready for multi-user testing

### Stage 2: Small Beta (1-3 Students)
**Status**: Planned

**Scope**:
- Instructor (Paul) tries system with 1-3 other students
- Test multi-user scenarios
- Gather feedback from instructor and students
- Identify multi-user requirements

**Key Features Needed**:
- User isolation (separate folders/repos per student)
- Instructor dashboard/access to all students
- Student-specific views
- Privacy and data organization

**Success Criteria**:
- System works for multiple students
- Instructor can manage multiple students
- Students have access to their own lessons
- Feedback incorporated

### Stage 3: Expanded Rollout
**Status**: Future

**Scope**:
- Expand to more students (10+)
- Scale system architecture
- Refine multi-user features
- Add collaboration features

**Success Criteria**:
- System scales to handle multiple students
- Performance remains good
- High user satisfaction
- Minimal support needed

### Stage 4: Teacher Global Library
**Status**: Future Vision

**Vision**: Build a comprehensive system for the instructor with:
- **Global Lesson Library**: Repository of all lessons across all students
- **Template System**: Reusable lesson plans that can be customized per student
- **Shared Song Library**: Database of songs with reusable charts and GuitarPro files
  - Charts and GP files can be reused across multiple lesson plans
  - Song metadata (key, tempo, difficulty, genre) for easy selection
  - Link existing charts/GP files when creating new lesson plans
- **Global Knowledge Base**: Music theory library shared across all students
- **Easy Customization**: Modify templates (change songs, adjust difficulty) for individual students
- **Lesson Plan Generation**: Web interface that pulls from global catalog to create new plans

**Example Workflow**:
1. Instructor creates "Bluegrass Basics" lesson plan template
2. Uses template for Student A → customize songs to: Dark Hollow, Nellie Kane
3. Uses same template for Student B → customize songs to: Big River, I'll Fly Away
4. Both students get personalized lessons from shared foundation
5. Instructor maintains one template, customizes per student

**Key Features**:
- Template inheritance system
- Shared vs. student-specific content management
- Easy customization workflow
- Version control for templates
- Global search across all students' lessons (for instructor)
- **Lesson Plan Generation Interface**:
  - Web-based interface for creating new lesson plans
  - Pulls from global catalog/library for content suggestions
  - Access to reusable song charts and GuitarPro files
  - AI-assisted generation with context from existing lessons
  - Template selection and customization
  - Smart content reuse (songs, exercises, concepts)

**Benefits**:
- Reduces instructor prep time
- Maintains consistency across students
- Allows personalization per student
- Builds comprehensive knowledge base
- Enables lesson plan reuse and refinement

**Technical Requirements**:
- Template system architecture
- Content inheritance/customization model
- Multi-tenant data organization
- Instructor admin interface
- Student-specific views
- **Lesson Plan Generation System**:
  - Web interface for lesson plan creation
  - AI prompt system for generating structured plans
  - Integration with global catalog/library APIs
  - Song selection with chart/GP file management
  - Template management and versioning
  - Content suggestion engine based on existing library

---

## Technical Stack Considerations

### Current
- Markdown files
- Git repository
- Manual AI prompt processing

### Future Considerations
- **Frontend**: React/Vue/Next.js (if web UI)
- **Backend**: Node.js/Python (for agents)
- **Message Bus**: NATS
- **Orchestration**: n8n or custom
- **Deployment**: Docker, Kubernetes (GKE)
- **Storage**: Git repo + potentially database for search
- **AI**: OpenAI API, Anthropic, or local models

---

## Success Metrics

### Phase 1 (Current)
- [ ] All lessons processed consistently
- [ ] Knowledge library growing and useful
- [ ] Clear workflow documented
- [ ] AI prompts produce quality results

### Phase 2
- [ ] File upload/management reduces friction
- [ ] Time to process lesson reduced
- [ ] Fewer manual steps required

### Phase 3
- [ ] Fully automated lesson processing
- [ ] Agents produce accurate, consistent results
- [ ] System scales to handle multiple lessons
- [ ] Minimal manual intervention needed

---

## Next Steps (Immediate)

1. **Continue manual processing** of lessons
2. **Refine AI prompt instructions** based on experience
3. **Document common patterns** and edge cases
4. **Evaluate file upload options** (web vs CLI)
5. **Research AI agent architectures** (n8n, K8s agents, NATS patterns)
6. **Review K8s AI agent webinar** if available

---

## Open Questions

- [ ] What's the preferred file upload approach?
- [ ] Should we start with n8n or go straight to custom agents?
- [ ] Do we need a database or is Git sufficient?
- [ ] How to handle version control with automated commits?
- [ ] What's the best way to validate AI agent outputs?
- [ ] Should agents be stateless or maintain context?

---

## Notes

- NATS experience: Used locally with Docker and in GKE - good fit for agent communication
- K8s AI agent webinar: Worth reviewing for architecture ideas
- Philosophy: Small, focused agents that do one thing well
- Current focus: Get manual process solid before automating
- Rollout strategy: Start with single user, expand to 1-3 students, then broader rollout, finally build global library for instructor
- Audio/Video: Currently transcript-based, future integration with farplay.io for multi-track audio and video analysis

