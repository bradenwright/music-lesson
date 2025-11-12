# AI Processing Instructions for Music Lessons

This document provides instructions for AI systems processing lesson transcripts and generating summaries, knowledge extractions, and documentation updates.

## Project Overview

This repository tracks bass lessons through multiple interconnected systems:
- **lesson-summary/**: Individual lesson summaries and transcripts
- **lesson-plans/**: Structured multi-lesson curricula
- **lesson-library/**: Searchable knowledge base of music theory concepts
- **songs/**: Song entries with notation, GuitarPro files, and lesson links

## Workflow for Processing a New Lesson

When processing a new lesson transcript, follow these steps in order:

### Step 1: Gather Context

**BEFORE processing the transcript, review:**

1. **Check for active lesson plans**:
   - Review files in `lesson-plans/` to identify any active curricula
   - Note which lesson number this session might correspond to
   - Understand the planned objectives and songs for that lesson

2. **Review previous lesson summaries**:
   - Check recent entries in `lesson-summary/` to understand progression
   - Note any ongoing assignments or topics

3. **Check existing songs**:
   - Review `songs/` directory to see which songs have been covered
   - Note if new songs are mentioned that need entries created

### Step 2: Process the Transcript

1. **Extract key information**:
   - Date of the lesson
   - Topics discussed
   - Songs covered or mentioned
   - Exercises assigned
   - Techniques practiced
   - Concepts explained
   - Homework/assignments given

2. **Identify lesson plan connections**:
   - Determine if this lesson corresponds to a specific lesson in a plan
   - Note which songs from the plan were covered
   - Track progress through the curriculum

3. **Identify knowledge to extract**:
   - Music theory concepts that should go in `lesson-library/`
   - Techniques that should be documented
   - Concepts about scales, harmony, genres, etc.

### Step 3: Generate Lesson Summary

Create a markdown file in `lesson-summary/` with the format: `YYYY-MM-DD.md`

**Required sections:**
- **Overview**: High-level summary of the lesson
- **Key Topics Discussed**: Organized by topic area
- **Songs Covered**: List with links to song entries (create if needed)
- **Practice Assignments**: Exercises, techniques, songs to practice
- **Next Steps**: Action items for student and teacher
- **Notes**: Any additional context or observations

**Linking requirements:**
- Link to relevant lesson plans in the progress tracking section
- Link to songs mentioned (format: `[Song Name](../songs/song-name/README.md)`)
- Link to lesson plan if part of a curriculum

### Step 4: Update or Create Song Entries

For each song mentioned in the lesson:

1. **Check if song entry exists** in `songs/song-name/`
2. **If exists**: Update the "Lesson Coverage" section with link to this lesson
3. **If new**: Create new song entry with:
   - Song information (artist, key, tempo, genre)
   - Lesson coverage section linking to this lesson
   - Links to relevant lesson plans
   - Practice notes specific to this song
   - Placeholders for images/ and guitarpro/ folders

**Song folder structure:**
```
songs/
  song-name/
    README.md
    images/          (for notation screenshots/photos)
    guitarpro/       (for .gp files)
```

### Step 5: Update Lesson Plan Progress

If this lesson is part of a structured lesson plan:

1. **Find the lesson plan** in `lesson-plans/`
2. **Update the Progress Tracking section**:
   - Replace the placeholder for the appropriate lesson number
   - Add link: `- **Lesson X**: [YYYY-MM-DD](../lesson-summary/YYYY-MM-DD.md)`
3. **Verify song links** in the plan point to correct song entries

### Step 6: Extract Knowledge for Library

Identify reusable concepts that should be added to `lesson-library/`:

**Categories to consider:**
- **scales-modes/**: Scale characteristics, moods, applications
- **harmony-theory/**: Chord progressions, resolution, tension, key changes
- **techniques/**: Playing techniques, practice methods, exercises
- **genres-styles/**: Genre-specific concepts
- **ear-training/**: Methods for developing musical ear

**For each concept:**
1. Determine the appropriate category folder
2. Check if a similar entry exists (update vs. create new)
3. Create/update markdown file with:
   - Concept overview
   - Key points and details
   - Examples if applicable
   - Related concepts
   - Source: link to lesson where learned

**Guidelines for extraction:**
- Extract concepts that are reusable and searchable
- Include context about when/where learned
- Cross-reference related concepts
- Focus on knowledge that will be useful for future reference

### Step 7: Quality Checks

Before finalizing, verify:

- [ ] All song mentions are linked to song entries
- [ ] Lesson plan progress tracking is updated if applicable
- [ ] Knowledge extracted to appropriate library folders
- [ ] All links use correct relative paths
- [ ] Date format is consistent (YYYY-MM-DD)
- [ ] Song folder names are lowercase with hyphens (e.g., `dark-hollow`)

## Example Processing Flow

**Input**: Transcript from lesson on 2024-10-22

**Context Gathering**:
- Review `lesson-plans/bluegrass-jamming-ear-training-6-lessons.md`
- Check if this is Lesson 1, 2, etc.
- Review previous lesson summary (2024-10-15.md)

**Processing**:
- Extract: covered Dark Hollow and Nellie Kane, worked on root notes
- Identify: This appears to be Lesson 1 of the bluegrass plan
- Extract knowledge: root note identification technique

**Outputs**:
1. Create `lesson-summary/2024-10-22.md` with summary
2. Update song entries for Dark Hollow and Nellie Kane with link to this lesson
3. Update lesson plan progress: `- **Lesson 1**: [2024-10-22](../lesson-summary/2024-10-22.md)`
4. Update `lesson-library/ear-training/root-note-identification.md` if new info

## Key Principles

1. **Always gather context first** - Review lesson plans and previous lessons before processing
2. **Maintain bidirectional links** - Songs link to lessons, lessons link to songs
3. **Extract reusable knowledge** - Don't just summarize, identify concepts for the library
4. **Track progress** - Update lesson plans to show actual progress through curriculum
5. **Be consistent** - Use consistent naming, formatting, and linking patterns

## File Naming Conventions

- **Lesson summaries**: `YYYY-MM-DD.md` (e.g., `2024-10-15.md`)
- **Song folders**: lowercase with hyphens (e.g., `dark-hollow`, `nellie-kane`)
- **Library entries**: descriptive lowercase with hyphens (e.g., `root-note-identification.md`)

## Link Format Examples

- Lesson summary to song: `[Dark Hollow](../songs/dark-hollow/README.md)`
- Lesson plan to summary: `[2024-10-15](../lesson-summary/2024-10-15.md)`
- Song to lesson: `[2024-10-15](../../lesson-summary/2024-10-15.md)`
- Library entry to lesson: `[2024-10-15](../../lesson-summary/2024-10-15.md)`

## Questions to Ask When Processing

- Is this lesson part of a structured plan? Which lesson number?
- What songs were covered? Do they have entries? Need to create?
- What reusable concepts were discussed? Where do they belong in the library?
- What techniques or exercises were introduced? Should they be documented?
- Are there connections to previous lessons or concepts already in the library?

