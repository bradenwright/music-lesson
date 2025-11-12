# Music Lessons - Bass Lesson Tracking System

This repository contains tools and documentation for tracking bass lessons, organizing music theory knowledge, and building a searchable library of musical concepts learned over time.

## Project Structure

### `lesson-summary/`
Contains AI-generated summaries and transcripts for each lesson session. Each lesson is stored with:
- **AI Summary**: High-level overview of what was covered
- **Transcript**: Full or processed transcript from the lesson recording
- **Markdown Files**: Detailed `.md` files covering topics discussed, exercises assigned, and progress notes

**Format**: Lessons are organized by date (e.g., `2024-10-15/`)

### `lesson-library/`
A searchable knowledge base of music theory concepts, techniques, and insights extracted from lessons. This is organized by topic areas such as:
- **Scales & Modes**: Information about different scales, their characteristics, moods, and applications
- **Harmony & Theory**: Concepts about chord progressions, resolution, tension, and key changes
- **Techniques**: Playing techniques, practice methods, and exercises
- **Genres & Styles**: Genre-specific concepts (bluegrass, jazz, etc.)
- **Ear Training**: Methods and concepts for developing musical ear

The library is designed to grow organically as new concepts are learned and can be reorganized as needed.

### `lesson-plans/`
Structured lesson plans that span multiple sessions. Each plan is a complete curriculum covering a specific topic or skill progression, including:
- Individual lesson breakdowns with objectives
- Progress tracking with links to actual lesson summaries
- Songs and exercises for each lesson
- Practice routines and homework assignments
- Song pools and reference materials

Lesson plans can link to completed lesson summaries to track progress through the curriculum.

## Workflow

1. **Record Lesson**: Record the lesson session (via Zoom or other method)
2. **Transcribe**: Process the recording to generate a transcript
3. **Generate Summary**: Use AI to create a summary and extract key concepts
4. **Store Summary**: Save summary and transcript in `lesson-summary/`
5. **Link to Lesson Plan**: If the lesson is part of a structured lesson plan, add a link to the lesson summary in the plan's progress tracking section
6. **Extract Knowledge**: Identify and extract reusable concepts for `lesson-library/`
7. **Update Library**: Add new concepts to appropriate folders in `lesson-library/`

## Goals

- Track lesson progress and assignments over time
- Build a personal music theory knowledge base
- Enable easy search and reference of concepts learned
- Support both structured learning and organic exploration
- Document teaching methodologies and practice techniques

## Future Enhancements

- Automated transcription pipeline
- AI-powered concept extraction from transcripts
- Search functionality across all lessons and library content
- Integration with practice tracking
- Audio/video analysis for technique feedback
