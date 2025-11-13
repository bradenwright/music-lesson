# Music Lessons Project Plan

## Project Overview

This project aims to create a comprehensive system for tracking bass lessons, organizing music theory knowledge, and eventually automating the processing of lesson content through specialized AI agents.

## Current State

### What We Have
- ✅ Project structure (lesson-summary, lesson-library, lesson-plans, songs)
- ✅ Comprehensive documentation (README, AI prompt instructions)
- ✅ Manual workflow for processing lessons
- ✅ Example lessons processed (2024-10-15 planning, 2024-10-22 Lesson 1)
- ✅ Knowledge library structure established

### What We're Building
- 🔄 Refining AI prompt instructions through experience
- 🔄 Processing more lessons to validate approach
- 📋 Planning automation pipeline

## Project Goals

### Short-term (Current Phase)
1. **Establish solid foundation**
   - Complete manual processing workflow
   - Refine AI prompt instructions
   - Process multiple lessons to identify patterns

2. **Document requirements**
   - Identify pain points in current process
   - Document edge cases and special scenarios
   - Define success criteria for automation

### Medium-term (Phase 2)
1. **Simplify file management**
   - Create tool/interface for uploading lesson files
   - Streamline preparation of files for AI processing
   - Reduce manual file organization steps

### Long-term (Phase 3+)
1. **Automate processing**
   - Build specialized AI agents
   - Create automated pipeline
   - Minimize manual intervention

## Current Workflow

### Manual Lesson Processing Steps
1. Receive lesson transcript/summary
2. Review lesson plans for context
3. Process transcript with AI using prompt instructions
4. Create lesson summary markdown
5. Update/create song entries
6. Update lesson plan progress tracking
7. Extract knowledge to library
8. Validate all links and references

### Pain Points Identified
- Manual file organization
- Copying/pasting between AI prompts
- Ensuring consistency across files
- Remembering all linking requirements
- Time-consuming for each lesson

## Automation Opportunities

### High Priority
1. **File Upload/Management**
   - Upload transcript, recordings, images
   - Auto-organize into correct folders
   - Generate initial file structure

2. **AI Processing Orchestration**
   - Automate passing files to AI
   - Handle multiple AI calls (summary, extraction, etc.)
   - Validate outputs

### Medium Priority
1. **Link Management**
   - Auto-generate links between files
   - Validate all links are correct
   - Update links when files move

2. **Knowledge Extraction**
   - Automatically identify concepts to extract
   - Categorize appropriately
   - Check for duplicates

### Lower Priority
1. **Git Integration**
   - Auto-commit processed lessons
   - Create PRs for review
   - Handle conflicts

2. **Search & Discovery**
   - Full-text search across all content
   - Related content suggestions
   - Progress tracking

## Technical Decisions Needed

### File Upload Solution
- **Option A**: Web frontend (React/Next.js)
- **Option B**: CLI tool/script
- **Option C**: Hybrid (start CLI, evolve to web)
- **Decision**: TBD - evaluate based on usage

### AI Agent Architecture
- **Option A**: n8n workflow
- **Option B**: Custom agents with NATS
- **Option C**: Kubernetes-based agents
- **Option D**: Hybrid approach
- **Decision**: TBD - research and prototype

### Storage
- **Current**: Git repository (markdown files)
- **Future**: May need database for search
- **Decision**: Start with Git, add DB if needed

## Implementation Phases

### Phase 1: Foundation (Current)
**Timeline**: Now - Until manual process is solid

**Tasks**:
- [x] Set up project structure
- [x] Create documentation
- [x] Process initial lessons
- [ ] Process 5-10 more lessons
- [ ] Refine AI prompts based on experience
- [ ] Document all edge cases
- [ ] Create comprehensive test cases

**Success Criteria**:
- Consistent, high-quality lesson summaries
- Knowledge library growing and useful
- Clear, documented workflow
- AI prompts produce reliable results

### Phase 2: File Management
**Timeline**: After Phase 1 complete

**Current Workflow (Phase 2A)**:
- **Status**: In use now
- **Process**: 
  - Teacher (Paul) emails lesson files (transcripts, recordings, images, GP files)
  - User (Braden) downloads files manually
  - User processes files with AI prompt
- **Purpose**: Simple, works for now, minimal setup required
- **Limitation**: Manual download and organization

**Future Workflow (Phase 2B - Phase 3 or later)**:
- **Goal**: Make it easier for teacher to upload files
- **Solution**: Simple web frontend
- **Features**:
  - Teacher uploads files via web interface
  - Files automatically uploaded to GCS (Google Cloud Storage)
  - App processes files from GCS
  - No manual download needed
- **Benefits**:
  - Teacher-friendly interface
  - Automated file handling
  - Files stored in cloud (GCS)
  - App can process directly from GCS
- **Timeline**: Phase 3 or after (when automation is ready)

**Tasks**:
- [x] Phase 2A: Manual email/download workflow (current)
- [ ] Phase 2B: Build simple web frontend for teacher
- [ ] Phase 2B: Integrate GCS upload
- [ ] Phase 2B: Update app to process from GCS
- [ ] Create AI prompt for lesson plan generation
- [ ] Build simple web interface for lesson plan creation

**Success Criteria**:
- Phase 2A: Manual workflow works reliably (current)
- Phase 2B: Teacher can upload files easily via web interface
- Phase 2B: Files automatically stored in GCS
- Phase 2B: App processes files from GCS automatically
- Reduces manual steps significantly

### Phase 2.5: Lesson Plan Generation
**Timeline**: Parallel to or after Phase 2

**Initial Approach: AI Prompt Interface**
- **Description**: Web interface with AI prompt to help generate lesson plan files
- **Features**:
  - Input form for lesson plan details (topic, duration, objectives, etc.)
  - AI prompt that generates structured lesson plan markdown
  - Outputs lesson plan file in correct format
  - Can download or save directly to repo
- **Use Case**: Instructor describes what they want to teach, AI generates structured lesson plan

**Future Integration (Phase 4)**:
- Pull from global catalog/library when building teacher's interface
- Access to all existing lesson plans as templates
- Access to global song library with charts and GP files
- Reuse existing content while creating new plans
- Smart suggestions based on previous lessons and student progress

### Phase 3: AI Automation
**Timeline**: After Phase 2 complete

**Implementation Progression**:

#### Phase 3A: Manual Processing (Current)
- **Process**: Manually copy/paste AI_PROMPT_INSTRUCTIONS.md into each prompt
- **Workflow**: Process each lesson manually with AI prompt
- **Status**: In use now
- **Purpose**: Validate workflow and refine instructions

#### Phase 3B: Agent Framework Integration
- **Process**: Use existing agent framework
- **Architecture**: 
  - Agent sends request to cursor-agent (requires Cursor IDE running locally)
  - cursor-agent processes using AI instructions and commands
  - Agent receives acknowledgment when complete
- **Key Change**: AI_PROMPT_INSTRUCTIONS.md content becomes part of agent's ai-instructions section
  - No longer need to manually copy/paste
  - Instructions embedded in agent configuration
- **Benefits**: 
  - Automated processing
  - Consistent instruction application
  - Still uses Cursor IDE infrastructure
- **Limitation**: Requires Cursor IDE running locally

#### Phase 3C: LLM/MCP Server Replacement
- **Process**: Replace cursor-agent with direct LLM call or MCP server
- **Options**:
  - Direct LLM API calls (OpenAI, Anthropic, etc.)
  - MCP (Model Context Protocol) server
  - Local LLM models
- **Benefits**:
  - No dependency on Cursor IDE
  - Can deploy independently
  - More flexible LLM provider choices
- **Future**: Can evolve to NATS-based microservices (Phase 3D)

#### Phase 3D: NATS-Based Microservices (Future)
- **Architecture**: NATS-based microservices (see PROJECT_ROADMAP.md for details)
- **Deployment**: Docker Compose for local, GKE for production
- **Agent Type**: Specialized agents for each task
- **Training**: Prompt engineering, RAG, fine-tuning as needed

**Tasks**:
- [x] Phase 3A: Manual processing (current)
- [ ] Phase 3B: Integrate with existing agent framework
  - [ ] Build lesson-plan-agent (interactive prompt for teacher/student)
  - [ ] Build lesson-summary-agent (process transcripts and files)
  - [ ] Build lesson-library-agent (extract permanent knowledge)
    - [ ] TBD: May call specialized topic agents (scales, music-theory, etc.) or delegate to separate agents
  - [ ] Build lesson-song-agent (or integrate into lesson-summary-agent)
- [ ] Phase 3C: Replace cursor-agent with LLM/MCP server
- [ ] Phase 3D: Build NATS-based microservices (optional future)

**Success Criteria**:
- Phase 3B: Automated processing via agent framework
- Phase 3C: Independent of Cursor IDE
- Phase 3D: Scalable microservices architecture
- Agents produce accurate results
- Minimal manual intervention

### Phase 4: Advanced Features
**Timeline**: After Phase 3 stable

**Tasks**:
- [ ] Add search functionality
- [ ] Audio/video analysis (see details below)
- [ ] Practice tracking integration
- [ ] Progress visualization
- [ ] Other enhancements as needed

### Phase 5: Audio/Video Recording & Analysis (Future)
**Timeline**: Long-term, after core system is stable

**Current State**: 
- Currently based on transcripts for lesson processing
- Manual transcription from recordings

**Future Vision: Audio/Video Recording Integration**

**Recording Tool: farplay.io**
- **Paid version features**:
  - Records video of lessons
  - Separate audio tracks for each participant
  - Ability to identify who's talking (speaker separation)
  - Separate audio track for bass instrument
  - Video recording for technique analysis

**Potential Use Cases**:

1. **Audio Alignment Analysis**
   - Compare student's bass playing with GuitarPro files
   - Analyze how well student plays along with backing tracks
   - Measure timing accuracy and rhythm alignment
   - Identify areas where student is ahead/behind the beat

2. **Technique Analysis from Video**
   - Analyze hand positioning and finger placement
   - Review posture and instrument positioning
   - Identify technique issues or improvements
   - Compare technique across lessons to track progress
   - Frame-by-frame analysis of specific techniques

3. **Multi-Track Audio Analysis**
   - Separate audio tracks allow for:
     - Isolating bass audio for detailed analysis
     - Comparing instructor's playing with student's
     - Analyzing timing and rhythm separately
     - Frequency analysis of bass tone and sound quality

4. **Enhanced Transcription**
   - Use separate audio tracks for better transcription accuracy
   - Speaker identification (instructor vs. student)
   - Better handling of overlapping speech
   - Music detection and separation from speech

5. **Progress Tracking**
   - Visual comparison of technique over time
   - Audio quality improvements tracking
   - Rhythm and timing accuracy metrics
   - Practice effectiveness measurement

6. **Interactive Ear Training Sessions (Gamified)**
   - **Training Mode**: Tones/notes are played, student tries to mimic on bass
   - **Real-time Feedback**: System analyzes if student played correct note/pitch
   - **Gamification Elements**: 
     - Score/points for accuracy
     - Progress tracking
     - Difficulty levels
     - Achievement system
   - **Multiple Reference Types** (can be toggled/changed):
     - **Notation**: Standard music notation display
     - **Color per Note**: Visual color coding for each note
     - **Tab**: Tablature display
     - **No Visual**: Audio only (pure ear training)
   - **Adaptive Learning**:
     - System can change which reference is shown
     - Gradually reduce visual aids as ear improves
     - Customize difficulty based on student progress
   - **Use Cases**:
     - Work on pitch recognition
     - Interval training
     - Scale recognition
     - Chord tone identification
     - Root note identification (building on existing ear training concepts)

**Technical Considerations**:
- Integration with farplay.io API or file export
- Storage of video and multi-track audio files
- Processing pipeline for audio/video analysis
- AI models for technique analysis
- Audio alignment algorithms
- Privacy and data management for video content
- **Ear Training System**:
  - Real-time audio analysis for pitch detection
  - Note recognition algorithms
  - Comparison between reference tone and student's playing
  - Visual rendering (notation, colors, tabs)
  - Gamification engine (scoring, progress, achievements)
  - Adaptive difficulty system
  - Integration with existing ear training concepts from library

**Challenges**:
- Large file sizes for video content
- Processing power for video analysis
- Privacy considerations with video recordings
- Cost of storage and processing
- Determining most valuable use cases before building

**Success Criteria**:
- Seamless recording integration
- Valuable insights from audio/video analysis
- Actionable feedback for student improvement
- Efficient storage and processing
- Clear use cases validated

## Rollout Strategy

### Phase 1: Single User (Current)
**Timeline**: Now - Until system is stable

**Scope**: 
- Braden (project owner) uses system for own lessons
- Manual processing and refinement
- Validate workflow and identify issues

**Success Criteria**:
- System works reliably for single user
- Workflow is clear and documented
- Quality outputs consistently produced

### Phase 2: Small Beta (1-3 Students)
**Timeline**: After Phase 1 stable

**Scope**:
- Instructor (Paul) tries system with 1-3 other students
- Test multi-user scenarios
- Gather feedback from instructor and students
- Refine based on real-world usage

**File Management**:
- **Current**: Teacher emails files, user downloads manually (Phase 2A)
- **Future**: Simple web frontend for teacher to upload to GCS (Phase 2B, Phase 3 or later)
- Files processed from GCS by app

**Considerations**:
- Need user isolation (separate folders/repos per student?)
- Instructor access to all student data
- Privacy and data organization
- Workflow adjustments for instructor perspective
- File upload workflow (email now, web frontend later)

**Success Criteria**:
- System works for multiple students
- Instructor can manage multiple students easily
- Students have access to their own lessons
- Feedback incorporated into improvements

### Phase 3: Expanded Rollout
**Timeline**: After Phase 2 successful

**Scope**:
- Expand to more students (10+)
- Scale system architecture if needed
- Refine multi-user features
- Add collaboration features as needed

**Success Criteria**:
- System scales to handle multiple students
- Performance remains good
- User satisfaction high
- Minimal support needed

### Phase 4: Teacher Global Library (Future)
**Timeline**: After Phase 3 stable

**Vision**:
- Build global library for instructor
- Shared lesson plans and templates
- Reusable knowledge base across all students
- Customization per student while maintaining shared resources

**Features**:
- **Global Lesson Library**: Instructor's repository of all lessons across students
- **Template System**: Create lesson plans that can be customized per student
- **Song Library**: Shared song database with student-specific notes
  - Reusable charts and GuitarPro files
  - Song metadata (key, tempo, difficulty, etc.)
  - Link to existing charts/GP files when creating new lesson plans
- **Knowledge Base**: Global music theory library with student-specific applications
- **Customization**: Ability to modify shared templates (change songs, adjust difficulty, etc.) for individual students
- **Lesson Plan Generation Interface**: 
  - Web-based interface for creating lesson plans
  - Pulls from global catalog/library for suggestions
  - Can reuse existing songs with their charts and GP files
  - AI-assisted generation with context from existing lessons

**Example Use Case**:
- Instructor has a "Bluegrass Basics" lesson plan template
- Uses it for Student A with songs: Dark Hollow, Nellie Kane
- Uses same template for Student B but changes songs to: Big River, I'll Fly Away
- Both students get personalized lessons from shared template
- Instructor maintains one template, customizes per student

**Technical Considerations**:
- Template system for lesson plans
- Inheritance/customization model
- Shared vs. student-specific content
- Version control for templates
- Easy customization workflow
- **Lesson Plan Generation**:
  - Web interface for creating lesson plans
  - AI prompt system that generates structured lesson plans
  - Integration with global catalog/library
  - Song selection interface with reusable charts and GP files
  - Template selection and customization

**Success Criteria**:
- Instructor can create reusable lesson templates
- Templates easily customizable per student
- Shared knowledge base benefits all students
- Reduces instructor prep time
- Maintains personalization for each student

## Risk Mitigation

### Risks Identified
1. **AI Quality**: Agents may not produce consistent results
   - *Mitigation*: Start with manual validation, refine prompts, add validation agents

2. **Complexity**: System may become too complex
   - *Mitigation*: Keep agents focused, simple interfaces, good documentation

3. **Maintenance**: Automated system requires ongoing maintenance
   - *Mitigation*: Good monitoring, logging, error handling

4. **Over-engineering**: Building too much too soon
   - *Mitigation*: Start simple, iterate based on actual needs

## Success Metrics

### Phase 1 Metrics
- Number of lessons processed
- Quality of summaries (subjective review)
- Knowledge library entries created
- Time per lesson processing

### Phase 2 Metrics
- Time saved on file management
- Reduction in manual steps
- User satisfaction with upload process

### Phase 3 Metrics
- Automation rate (% of lessons fully automated)
- Accuracy of agent outputs
- Time to process lesson
- Manual intervention frequency

## Next Actions

### This Week
1. Continue processing lessons manually
2. Note any issues or improvements needed
3. Update AI prompt instructions as needed

### This Month
1. Process 5-10 more lessons
2. Document all patterns and edge cases
3. Evaluate file upload options
4. Research AI agent architectures

### This Quarter
1. Decide on file upload approach
2. Build file management solution
3. Begin prototyping AI agents
4. Test with real data

## Resources & References

- **NATS**: Message bus for agent communication (experience with Docker and GKE)
- **K8s AI Agents Webinar**: Review for architecture ideas
- **n8n**: Workflow automation platform (evaluate for orchestration)
- **Current Repo**: Foundation for all content

## Notes

- Philosophy: Small, focused agents that excel at specific tasks
- Communication: NATS proven to work well for microservices
- Current focus: Get manual process perfect before automating
- Future vision: Fully automated pipeline with specialized AI agents
- Rollout: Start small (single user), expand gradually, build global library for instructor
- Audio/Video: Currently transcript-based, future integration with farplay.io for rich media analysis

