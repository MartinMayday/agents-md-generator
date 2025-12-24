# Framework Definition: AGENTS.md Generator

**Version:** 1.0.0  
**Date:** [DATE]  
**Status:** Framework Definition  
**Purpose:** Define the AGENTS.md Generator framework for platforms supporting only AI/LLM + prompting + file uploads

---

## What This Framework Does

The **AGENTS.md Generator Framework** is a systematic approach to automatically generate production-ready `AGENTS.md` files for any folder containing markdown documentation. The framework transforms folder contents into structured, vendor-neutral context files that AI/LLM agents can use for efficient progressive context loading.

### Core Purpose

[FRAMEWORK_CORE_PURPOSE - Describe the primary purpose: e.g., "Transform folder contents into structured, vendor-neutral context files that AI/LLM agents can use for efficient progressive context loading, reducing context bloat by 85% while maintaining complete traceability."]

### Key Principles

1. **Progressive Context Loading** - All generated AGENTS.md files include a CONTEXT section with 4 levels (Front Matter, AGENTS.md Content, Reference Files, Source Code Execution)
2. **Vendor-Neutral** - Follows AGENTS.md best practices recognized by GitHub Copilot, Cursor, Windsurf, Claude Code, and other AI tools
3. **Template-Driven** - Uses a structured template with placeholders to ensure consistency
4. **Validation-Based** - Includes comprehensive validation checks to ensure quality
5. **Zero Assumptions** - All content must come from actual files or extracted data, not assumptions

### What It Generates

The framework generates `AGENTS.md` files that include:

- **YAML Frontmatter** - Metadata (title, version, date, status, classification)
- **Contextual Snippets** - Brief descriptions for Level 1 context loading (~200 tokens)
- **File Inventory** - Complete list of all markdown files with purpose, use_when, tier, word_count
- **Key Concepts** - 3-10 core concepts extracted from folder content
- **Expected Outcomes** - 3-5 outcomes derived from folder purpose
- **CONTEXT Section** - Progressive context loading protocol with 4 levels
- **Document Guide** - Detailed breakdown of each file (Purpose, Contains, Use When, Key Sections)
- **Quick Start** - Workflow for AI agents to use the generated AGENTS.md
- **Quality Guarantees** - Standards and enforcement methods

### Benefits

- **85% Context Reduction** - Progressive loading vs. loading everything upfront
- **Auto-Discovery** - AI tools automatically detect and use AGENTS.md files
- **Vendor-Neutral** - Works with all major AI coding tools
- **Complete Documentation** - Every file documented with specific purposes and use cases
- **Zero Context ROT** - All content traceable to actual files

---

## Use Cases

### Use Case 1: Generate AGENTS.md for a Documentation Folder

**Scenario:** [USE_CASE_1_SCENARIO - e.g., "You have a documentation folder containing multiple markdown files explaining a framework, tool, or methodology. You want AI agents to automatically discover and use this documentation efficiently."]

**Input:**
- Folder path: `[FOLDER_PATH_1]`
- Folder contains: [LIST_FILES_1 - e.g., "README.md, QUICK-START.md, API-REFERENCE.md, EXAMPLES.md, TROUBLESHOOTING.md"]
- Folder purpose: [FOLDER_PURPOSE_1 - e.g., "Documentation for a framework that helps developers build AI agents"]

**Process:**
1. **Analysis Phase** - Analyze folder structure and identify all markdown files
2. **Extraction Phase** - Extract contextual snippets, keywords, and determine tier assignments
3. **Generation Phase** - Fill template with extracted data to generate AGENTS.md
4. **Validation Phase** - Validate generated AGENTS.md against quality gates
5. **Refinement Phase** - Fix any issues and re-validate

**Output:**
- `[FOLDER_PATH_1]/AGENTS.md` - Production-ready AGENTS.md file
- File includes: [OUTPUT_DETAILS_1 - e.g., "Complete file inventory, progressive context loading protocol, document guide for each file, key concepts, expected outcomes"]

**Example Result:**
```yaml
# Example contextual snippet from generated AGENTS.md
contextual_snippets:
  - snippet: "[SNIPPET_1 - First sentence from README.md]"
    keywords: [KEYWORD_1, KEYWORD_2, KEYWORD_3]
    file: README.md
    tier: 1
```

---

### Use Case 2: Generate AGENTS.md for a Project with Multiple Modules

**Scenario:** [USE_CASE_2_SCENARIO - e.g., "You have a project folder with multiple modules, each containing documentation. You want AI agents to understand the project structure and navigate between modules efficiently."]

**Input:**
- Folder path: `[FOLDER_PATH_2]`
- Folder contains: [LIST_FILES_2 - e.g., "README.md, module-a/README.md, module-b/README.md, module-c/README.md, ARCHITECTURE.md"]
- Folder purpose: [FOLDER_PURPOSE_2 - e.g., "Multi-module project with separate documentation for each module"]

**Process:**
1. **Analysis Phase** - Analyze folder structure, identify modules and their documentation
2. **Extraction Phase** - Extract context from each module, assign tiers based on importance
3. **Generation Phase** - Generate AGENTS.md with module-specific sections
4. **Validation Phase** - Validate structure and content quality
5. **Refinement Phase** - Ensure module relationships are clear

**Output:**
- `[FOLDER_PATH_2]/AGENTS.md` - AGENTS.md with module-specific documentation
- File includes: [OUTPUT_DETAILS_2 - e.g., "Module inventory, cross-module references, tier assignments for each module, progressive loading for module-specific content"]

**Example Result:**
```markdown
## Document Guide

### 1. README.md — Project Overview
**Purpose:** [PURPOSE_2_1 - Main project overview]
**Tier:** 1 (Essential - Load First)

### 2. module-a/README.md — Module A Documentation
**Purpose:** [PURPOSE_2_2 - Module A specific purpose]
**Tier:** 2 (Core - Load on Demand)
```

---

### Use Case 3: Generate AGENTS.md for a Framework/Toolkit Folder

**Scenario:** [USE_CASE_3_SCENARIO - e.g., "You have a framework or toolkit folder with comprehensive documentation including guides, templates, examples, and reference materials. You want AI agents to understand the framework structure and use it effectively."]

**Input:**
- Folder path: `[FOLDER_PATH_3]`
- Folder contains: [LIST_FILES_3 - e.g., "README.md, GETTING-STARTED.md, TEMPLATE.md, EXAMPLES.md, API-REFERENCE.md, BEST-PRACTICES.md"]
- Folder purpose: [FOLDER_PURPOSE_3 - e.g., "Framework for building AI agent workflows with templates and examples"]

**Process:**
1. **Analysis Phase** - Analyze framework structure, identify core vs. reference documentation
2. **Extraction Phase** - Extract framework concepts, key features, usage patterns
3. **Generation Phase** - Generate AGENTS.md with framework-specific structure
4. **Validation Phase** - Validate framework concepts and usage examples
5. **Refinement Phase** - Ensure framework workflow is clear

**Output:**
- `[FOLDER_PATH_3]/AGENTS.md` - Framework-specific AGENTS.md
- File includes: [OUTPUT_DETAILS_3 - e.g., "Framework overview, key concepts, usage workflow, template references, example scenarios, progressive loading for framework components"]

**Example Result:**
```markdown
## Key Concepts
- "[CONCEPT_1 - Core framework concept]"
- "[CONCEPT_2 - Another framework concept]"
- "[CONCEPT_3 - Framework pattern or principle]"

## Expected Outcomes
- "[OUTCOME_1 - What users can achieve with this framework]"
- "[OUTCOME_2 - Another expected result]"
```

---

## Template

The following template structure should be used to generate AGENTS.md files. Replace all `[PLACEHOLDER]` text with actual content extracted from the target folder.

### YAML Frontmatter Template

```yaml
---
title: [FOLDER_TITLE]
version: [VERSION]
author: [AUTHOR]
date: [DATE]
status: [STATUS]
classification: Internal Operations | Handoff to IDE/CLI AI Coders
framework: [FRAMEWORK]
project: [PROJECT_NAME]
output_expected: [OUTPUT_EXPECTED]
execution_time: [EXECUTION_TIME]

# Contextual Retrieval Snippets (Level 1: Always Loaded)
contextual_snippets:
  - snippet: "[FILE_PURPOSE - first sentence or summary from file]"
    keywords: [KEYWORDS - array of 3-10 relevant keywords from file]
    file: [FILE_NAME]
    tier: [TIER_ASSIGNMENT - 1, 2, or 3]
  # ADD MORE: One entry per markdown file in folder

# File Inventory
files:
  - name: [FILE_NAME]
    purpose: "[FILE_PURPOSE - specific and actionable, not vague]"
    use_when: "[USE_WHEN - scenario-based, clear when to use this file]"
    tier: [TIER_ASSIGNMENT - 1=essential, 2=core, 3=reference]
    word_count: [WORD_COUNT - actual word count from file]
  # ADD MORE: One entry per markdown file in folder

# Key Concepts
key_concepts:
  - "[KEY_CONCEPT_1 - specific concept extracted from folder content]"
  - "[KEY_CONCEPT_2 - another core concept]"
  - "[KEY_CONCEPT_3 - continue as needed]"
  # ADD MORE: 3-10 concepts total

# Expected Outcomes
outcomes:
  - "[OUTCOME_1 - what users can achieve with this package]"
  - "[OUTCOME_2 - another expected result]"
  - "[OUTCOME_3 - continue as needed]"
  # ADD MORE: 3-5 outcomes total
---
```

### Main Content Template

```markdown
# [FOLDER_TITLE]

**[FOLDER_DESCRIPTION - one sentence summary of what this folder contains]**

**Version:** [VERSION]  
**Status:** [STATUS]  
**Framework:** [FRAMEWORK - if applicable]  
**Target:** [TARGET - what this package is for]

---

## 📋 Overview

[OVERVIEW_TEXT - 2-3 paragraphs explaining what this folder contains, its purpose, and key features. Extract from folder analysis and README files if present.]

**Core Purpose:** [CORE_PURPOSE - one sentence describing the primary purpose]

**Key Outcome:** [KEY_OUTCOME - one sentence describing the expected result]

---

## 🎯 CONTEXT: Progressive Context Loading Protocol

This section implements **progressive context loading** as described in [Claude Agent Skills: Teaching Your AI Agent to Wear Multiple Hats](https://cloudnativeengineer.substack.com/p/ai-agent-wear-multiple-hats?open=false#%C2%A7how-progressive-context-loading-works). Context loads in stages to prevent bloat and ensure only relevant information is loaded when needed.

### Level 1: Front Matter (Always Loaded) - ~200 tokens

**When:** Every conversation start  
**Token Cost:** ~200 tokens  
**Load Time:** Instant

**Content:**
- Package title and description (from YAML frontmatter)
- Key concepts (one-line summaries)
- Expected outcomes (bullet points)
- Contextual snippets (brief descriptions only)

**Purpose:** AI agent decides "Should I use this package?" without loading full content.

**Example:**
```yaml
contextual_snippets:
  - snippet: "[EXAMPLE_SNIPPET - brief description]"
    keywords: [EXAMPLE_KEYWORDS]
    file: [EXAMPLE_FILE]
    tier: 1
```

---

### Level 2: AGENTS.md Content (On-Demand) - ~2,000 tokens

**When:** After AI agent confirms package is relevant  
**Token Cost:** ~2,000 tokens  
**Load Time:** < 1 second  
**Trigger:** AI asks: "Load full package instructions? (Takes ~2000 tokens)"

**Content:**
- Complete file inventory with purpose and use_when
- Document Guide section (detailed breakdown of each file)
- Quick Start workflow
- Key principles and quality guarantees
- Execution checklist

**Purpose:** Full package instructions without loading individual file contents.

**What's Included:**
- File descriptions (purpose, use_when, tier, word_count)
- Document Guide for each file (Purpose, Contains, Use When, Key Sections)
- Execution workflow diagram
- Quality guarantees table
- Key principles

**What's NOT Included:**
- Full content of individual files
- Detailed code examples
- Complete templates

---

### Level 3: Reference Files (Selectively Loaded) - Variable tokens

**When:** Specific file content needed during execution  
**Token Cost:** Variable (500-12,000 tokens per file)  
**Load Time:** < 1 second per file  
**Trigger:** AI asks: "Load [filename] for [specific task]? (Takes ~X tokens)"

**Content:**
- Individual file contents loaded only when referenced
- Detailed guides, templates, examples
- Complete specifications and frameworks

**File Loading Tiers:**

**Tier 1 Files (Load First - Essential):**
[TIER_1_FILES - list files with tier 1, include word counts]
- `[FILE_NAME]` (~[WORD_COUNT] words) - [BRIEF_PURPOSE]

**Tier 2 Files (Load on Demand - Core Execution):**
[TIER_2_FILES - list files with tier 2, include word counts]
- `[FILE_NAME]` (~[WORD_COUNT] words) - [BRIEF_PURPOSE]

**Tier 3 Files (Load Only When Needed - Historical/Reference):**
[TIER_3_FILES - list files with tier 3, include word counts]
- `[FILE_NAME]` (~[WORD_COUNT] words) - [BRIEF_PURPOSE]

**Purpose:** Detailed content appears only when explicitly needed, keeping context clean.

**Example Loading Sequence:**
```
User: "I need to execute Phase 1"
↓
AI: "Load [TIER_1_FILE]? (Takes ~[WORD_COUNT] tokens)"
↓
User: "Yes"
↓
AI loads: [TIER_1_FILE] (Level 3)
↓
AI: "Load [TIER_2_FILE] Phase 1 section? (Takes ~[WORD_COUNT] tokens)"
↓
User: "Yes"
↓
AI loads: Phase 1 section only (Level 3, selective)
```

---

### Level 4: Source Code (Execute, Don't Load) - ~100 tokens output only

**When:** Validation scripts need to run  
**Token Cost:** ~100 tokens (output only, code not loaded)  
**Load Time:** Execution time (varies)  
**Trigger:** AI executes: `python validation/validate-story-file.py story.md`

**Content:**
- Python validation scripts (execute, don't load to context)
- Script output (success/failure messages)
- Metrics and reports (generated data)

**Purpose:** Complex logic stays external, keeping context window clean.

**What's Executed:**
[LIST_SCRIPTS - if folder contains Python scripts, list them here]
- `[SCRIPT_NAME].py` - [SCRIPT_PURPOSE]

**What's Loaded:**
- Only script output (✅/❌, error messages, metrics)
- Never the script source code itself

**Example:**
```bash
# AI executes (code not loaded to context):
python validation/validate-story-file.py stories/story_city001.md

# AI sees only output (~100 tokens):
✅ Valid - All 7 sections present, testable
Section 1: REQUIREMENTS ✅
Section 2: DESIGN DECISIONS ✅
...
```

---

### Progressive Loading Summary

| Level | Content | Token Cost | When | Trigger |
|-------|---------|------------|------|---------|
| **1. Front Matter** | Brief description, keywords | ~200 | Always | Automatic |
| **2. AGENTS.md** | Full package instructions | ~2,000 | On-demand | AI confirms relevance |
| **3. Reference Files** | Individual file contents | 500-12,000 | Selective | AI asks per file |
| **4. Source Code** | Script execution output | ~100 | As needed | AI executes scripts |

**Total Maximum Context:** ~[MAX_TOKENS] tokens (if all files loaded)  
**Typical Context:** ~2,200 tokens (Level 1 + Level 2 only)  
**Context Savings:** [SAVINGS_PERCENT]% reduction vs. loading everything upfront

---

## 📚 Document Guide

# REPLACE: [FILE_NAME], [FILE_PURPOSE], [CONTAINS], [USE_WHEN], [KEY_SECTIONS], [TIER], [WORD_COUNT]
# GENERATE: One Document Guide section per file in folder
# FORMAT: Follow the pattern below for each file

### 1. **[FILE_NAME]** — [FILE_PURPOSE_SHORT]

**Purpose:** [FILE_PURPOSE - full purpose statement]

**Contains:**
- [CONTAINS_ITEM_1 - main content element]
- [CONTAINS_ITEM_2 - another content element]
- [CONTAINS_ITEM_3 - continue as needed]
- [ADD_MORE - extract from actual file content]

**Use When:**
- [USE_WHEN_SCENARIO_1 - specific scenario]
- [USE_WHEN_SCENARIO_2 - another scenario]
- [USE_WHEN_SCENARIO_3 - continue as needed]

**Key Sections:**
- [KEY_SECTION_1 - main section name]
- [KEY_SECTION_2 - another section]
- [KEY_SECTION_3 - continue as needed]

**Context Loading Tier:** [TIER_ASSIGNMENT] ([TIER_DESCRIPTION])

**Word Count:** ~[WORD_COUNT] words

---

# REPEAT: Generate one Document Guide section for each file in folder
# Use the same format as above for each file

---

## 🚀 Quick Start (5 Minutes)

### Step 1: Load Level 1 Context (Automatic)
AI agent automatically loads front matter:
- Package description
- Key concepts
- Expected outcomes
- Contextual snippets

**Token Cost:** ~200 tokens  
**Time:** Instant

### Step 2: Confirm Package Relevance
AI asks: "This package [BRIEF_DESCRIPTION]. Should I load full instructions? (~2000 tokens)"

**If Yes:** Proceed to Step 3  
**If No:** AI suggests alternative or asks for clarification

### Step 3: Load Level 2 Context (On-Demand)
AI loads full AGENTS.md content:
- Complete file inventory
- Document Guide
- Quick Start workflow
- Key principles

**Token Cost:** ~2,000 tokens  
**Time:** < 1 second

### Step 4: Execute Based on Need
**For Execution:**
1. AI loads [TIER_1_FILE] (Level 3, ~[WORD_COUNT] tokens)
2. AI loads [TIER_2_FILE] specific section (Level 3, ~[WORD_COUNT] tokens)
3. Execute task
4. Continue with additional files as needed

**For Reference:**
1. AI loads [TIER_3_FILE] specific section (Level 3, variable tokens)
2. AI loads [ANOTHER_FILE] if overview needed (Level 3, variable tokens)

**For Validation:**
1. AI executes validation scripts (Level 4, ~100 tokens output only)
2. AI sees results, code not loaded to context

---

## 📊 Expected Output Structure

[OUTPUT_STRUCTURE - if applicable, describe what this package generates or contains. Extract from folder analysis.]

**Total:** [FILE_COUNT] files, ~[TOTAL_WORDS] words, [QUALITY_STANDARD]

---

## ✅ Quality Guarantees

| Guarantee | Standard | Enforcement |
|-----------|----------|-------------|
| **No Context ROT** | 0% hallucinations | [VALIDATION_METHOD] |
| **Progressive Loading** | 4-level system | CONTEXT section |
| **Complete Documentation** | All files documented | File inventory |
| **Accurate Metadata** | ±10% word count tolerance | Validation scripts |

---

## 🚀 Key Principles

### 1. PROGRESSIVE CONTEXT LOADING
Context loads in stages (prevent ROT):
- **Level 1:** Front matter (200 tokens) - Always loaded
- **Level 2:** AGENTS.md content (2,000 tokens) - On-demand
- **Level 3:** Reference files (500-12,000 tokens) - Selective
- **Level 4:** Source code execution (~100 tokens output) - Execute, don't load

### 2. VENDOR-NEUTRAL
Follow AGENTS.md best practices:
- Recognized by GitHub Copilot, Cursor, Windsurf, Claude Code
- No tool-specific terminology
- Generic AI/LLM agent language

### 3. COMPLETE DOCUMENTATION
Every file documented:
- Specific purpose (not vague)
- Scenario-based use_when statements
- Accurate metadata (word counts, tiers)

---

## 📋 Execution Checklist

**Before starting:**
- [ ] All files downloaded/accessible
- [ ] Read overview (10 min)
- [ ] Understand progressive loading protocol
- [ ] Ready to execute

**After execution:**
- [ ] All files loaded as needed
- [ ] Progressive loading worked correctly
- [ ] Context savings achieved
- [ ] Mission complete

---

## 📞 Support

During execution, if you get stuck:

1. **Check Document Guide** - Detailed file breakdowns
2. **Review CONTEXT section** - Progressive loading protocol
3. **Reference file inventory** - Find right file for task
4. **Check tier assignments** - Load files in correct order

---

## 🎯 Success Signal

When AI agent successfully uses this package:

```
✅ Level 1 context loaded (200 tokens)
✅ Level 2 context loaded (2000 tokens)
✅ Level 3 files loaded selectively as needed
✅ Context savings: [PERCENT]% reduction
✅ Mission complete
```

**Status:** Ready for use by AI/LLM agents

---

## 📚 File Reference Quick Links

[QUICK_LINKS - generate links to all files in folder]
- **[Start Here]:** `[TIER_1_FILE]`
- **[Execute This]:** `[TIER_2_FILE]`
- **[Reference This]:** `[TIER_3_FILE]`
- **[Add More]:** `[OTHER_FILES]`

---

## 📖 References

- [Claude Agent Skills: Teaching Your AI Agent to Wear Multiple Hats](https://cloudnativeengineer.substack.com/p/ai-agent-wear-multiple-hats?open=false#%C2%A7how-progressive-context-loading-works) - Progressive context loading framework
- [Equipping Agents for the Real World with Agent Skills](https://www.anthropic.com/research/equipping-agents) - Anthropic's official skills architecture
- [Agent Skills Best Practices](https://docs.anthropic.com/claude/docs/agent-skills) - Official documentation

---

**Generated:** [DATE]  
**Status:** [STATUS]  
**Quality:** Progressive context loading, complete traceability  
**Next:** Use by AI/LLM agents for efficient context management

**Ready for use.** 🚀
```

---

## Execution Strategy (No Code Execution)

For platforms that only support AI/LLM + prompting + file uploads (no code execution), follow this manual execution strategy:

### Phase 1: Manual Folder Analysis

**Objective:** Understand folder structure and identify all markdown files

**Steps:**
1. **List all files** in the target folder
   - Identify all `.md` files
   - Note file sizes and modification dates
   - Identify file relationships (README, guides, examples, etc.)

2. **Read file headers** (first 100-200 words of each file)
   - Extract titles and descriptions
   - Identify file types (README, guide, template, example, etc.)
   - Note any YAML frontmatter

3. **Create file inventory** manually:
   ```markdown
   Files found:
   - README.md (~[WORD_COUNT] words) - Main overview
   - QUICK-START.md (~[WORD_COUNT] words) - Getting started guide
   - [ADD_MORE_FILES]
   ```

**What to Upload:**
- Upload folder structure listing
- Upload first 200 words of each markdown file
- Upload any README or overview files completely

---

### Phase 2: Manual Context Extraction

**Objective:** Extract contextual snippets, keywords, and determine tier assignments

**Steps:**
1. **Extract snippets** (first meaningful paragraph from each file)
   - Read first 200-500 words of each file
   - Extract first complete sentence or paragraph
   - Remove markdown formatting
   - Limit to 200 characters

2. **Extract keywords** (3-10 per file)
   - From file titles/headings
   - From YAML frontmatter (if present)
   - From first paragraph content
   - From file purpose

3. **Assign tiers** based on file importance:
   - **Tier 1 (Essential):** README, quick-start, overview files
   - **Tier 2 (Core):** Main guides, templates, execution files
   - **Tier 3 (Reference):** Examples, historical logs, detailed references

4. **Determine file purposes** (specific and actionable)
   - Read file content to understand purpose
   - Avoid vague descriptions like "Documentation"
   - Use specific descriptions like "Step-by-step execution instructions for Phase 1"

5. **Create use_when statements** (scenario-based)
   - Based on file content analysis
   - Use format: "When [specific scenario], use this file for [specific purpose]"
   - Avoid generic statements like "When needed"

**What to Upload:**
- Upload full content of each markdown file (or at least first 1000 words)
- Upload extracted snippets for verification
- Upload tier assignments with reasoning

---

### Phase 3: Manual Template Filling

**Objective:** Fill template with extracted data to generate AGENTS.md

**Steps:**
1. **Load template** (use template section above)
   - Copy the complete template structure
   - Identify all placeholders

2. **Replace YAML frontmatter placeholders:**
   - `[FOLDER_TITLE]` → Extract from folder name or README title
   - `[VERSION]` → Use "1.0.0" or extract from metadata
   - `[DATE]` → Current date (YYYY-MM-DD)
   - `[STATUS]` → "Production Ready" or extract from folder
   - `[FRAMEWORK]` → Extract from folder content analysis
   - `[PROJECT_NAME]` → Extract from folder name or metadata

3. **Fill contextual snippets:**
   - Use snippets extracted in Phase 2
   - One entry per markdown file
   - Include keywords and tier assignments

4. **Fill file inventory:**
   - Use file analysis from Phase 1
   - Use purposes and use_when from Phase 2
   - Include word counts (estimate if needed)

5. **Extract key concepts:**
   - Read folder content to identify 3-10 core concepts
   - Concepts should be specific to folder content
   - Avoid generic concepts

6. **Determine expected outcomes:**
   - Based on folder purpose
   - 3-5 outcomes describing what users can achieve
   - Specific and actionable

7. **Fill Document Guide sections:**
   - For each file, read content to extract:
     - "Contains" - List main content elements
     - "Key Sections" - List main headings
     - "Use When" - Specific scenarios
   - **CRITICAL:** Read actual file content, don't assume

8. **Fill CONTEXT section:**
   - List Tier 1, 2, 3 files with word counts
   - Calculate token costs
   - Calculate context savings percentage

**What to Upload:**
- Upload filled template for review
- Upload source files used for extraction
- Upload any validation notes

---

### Phase 4: Manual Validation

**Objective:** Validate generated AGENTS.md against quality gates

**Validation Checklist:**

1. **YAML Frontmatter:**
   - [ ] YAML syntax is valid (check with YAML parser if available)
   - [ ] All required fields present (title, version, date, status, classification)
   - [ ] Field values are valid (non-empty, proper format)

2. **Required Sections:**
   - [ ] CONTEXT section present with all 4 levels
   - [ ] Document Guide section present
   - [ ] File inventory present in YAML
   - [ ] Contextual snippets present in YAML

3. **Tier Assignments:**
   - [ ] All tiers are 1, 2, or 3
   - [ ] Tier assignments are logical
   - [ ] Tier 1 files are truly essential

4. **Content Quality:**
   - [ ] No placeholder text remains (search for `[` in file)
   - [ ] File purposes are specific (not "Documentation")
   - [ ] use_when statements are scenario-based
   - [ ] Snippets match actual file content
   - [ ] Document Guide sections reference actual file content

5. **File Inventory:**
   - [ ] All markdown files in folder are listed
   - [ ] Word counts are reasonable (±10% tolerance)
   - [ ] File names are accurate

6. **Progressive Loading:**
   - [ ] All 4 levels documented
   - [ ] Token costs specified
   - [ ] Triggers specified
   - [ ] Context savings calculated

**What to Upload:**
- Upload validation checklist results
- Upload any issues found
- Upload corrected AGENTS.md if fixes needed

---

### Phase 5: Refinement (If Needed)

**Objective:** Fix any issues identified during validation

**Steps:**
1. **Review validation results**
   - Identify failed checks
   - Prioritize fixes

2. **Fix issues:**
   - Replace remaining placeholders
   - Correct tier assignments
   - Improve file purposes (make specific)
   - Update use_when statements (make scenario-based)
   - Verify snippets match actual content
   - Verify Document Guide sections match actual files

3. **Re-validate:**
   - Run validation checklist again
   - Verify all checks pass

4. **Final review:**
   - Read generated AGENTS.md completely
   - Verify content quality
   - Ensure no assumptions remain

**What to Upload:**
- Upload refined AGENTS.md
- Upload validation results showing all checks pass

---

## Placeholder Replacement Guide

This guide explains how to replace each placeholder in the template with actual content.

### YAML Frontmatter Placeholders

| Placeholder | Source | Example |
|------------|--------|---------|
| `[FOLDER_TITLE]` | Folder name or README title | "AGENTS.md Generator SOP" |
| `[VERSION]` | Use "1.0.0" or extract from metadata | "1.0.0" |
| `[AUTHOR]` | Extract from folder metadata or use "AI Agent" | "AI Agent" |
| `[DATE]` | Current date (YYYY-MM-DD) | "2025-12-23" |
| `[STATUS]` | "Production Ready" or extract from folder | "Production Ready" |
| `[FRAMEWORK]` | Extract from folder content analysis | "AGENTS.md Generation with Progressive Context Loading" |
| `[PROJECT_NAME]` | Extract from folder name or metadata | "agents-md-generator" |
| `[OUTPUT_EXPECTED]` | Describe what this package contains/generates | "Production-ready AGENTS.md files with progressive context loading" |
| `[EXECUTION_TIME]` | Estimate time to use this package | "5-15 minutes per folder" |

### Contextual Snippets Placeholders

| Placeholder | Source | Example |
|------------|--------|---------|
| `[FILE_NAME]` | Actual filename from folder | "README.md" |
| `[FILE_PURPOSE]` | First sentence or summary from file content | "Complete Standard Operating Procedure for automatically generating production-ready AGENTS.md files" |
| `[KEYWORDS]` | Array of 3-10 keywords extracted from file | `[sop, agents.md, generation, progressive context loading]` |
| `[TIER_ASSIGNMENT]` | 1, 2, or 3 based on file importance | `1` |

**How to Extract:**
1. Read first 200-500 words of file
2. Extract first complete sentence or paragraph
3. Remove markdown formatting
4. Limit to 200 characters
5. Extract keywords from titles, headings, frontmatter, content

### File Inventory Placeholders

| Placeholder | Source | Example |
|------------|--------|---------|
| `[FILE_NAME]` | Actual filename | "README.md" |
| `[FILE_PURPOSE]` | Specific, actionable purpose statement | "Overview and quick start guide for the entire SOP" |
| `[USE_WHEN]` | Scenario-based statement | "First time using the tool, need orientation and understanding of package contents" |
| `[TIER_ASSIGNMENT]` | 1, 2, or 3 | `1` |
| `[WORD_COUNT]` | Actual word count from file | `1864` |

**How to Determine:**
- **Purpose:** Read file content, identify specific purpose (not "Documentation")
- **Use When:** Based on file content, create scenario-based statements
- **Tier:** Assign based on importance (1=essential, 2=core, 3=reference)
- **Word Count:** Count words in file (estimate if needed, ±10% tolerance)

### Content Placeholders

| Placeholder | Source | Example |
|------------|--------|---------|
| `[FOLDER_DESCRIPTION]` | One sentence summary | "A complete framework for automatically generating production-ready AGENTS.md files" |
| `[OVERVIEW_TEXT]` | 2-3 paragraphs from folder analysis | Extract from README or main files |
| `[CORE_PURPOSE]` | One sentence primary purpose | "Transform folder contents into structured, vendor-neutral context files" |
| `[KEY_OUTCOME]` | One sentence expected result | "Generate AGENTS.md files with zero context ROT and complete file inventory" |
| `[KEY_CONCEPTS]` | 3-10 concepts from content analysis | "5-phase workflow: Analyze → Extract → Generate → Validate → Refine" |
| `[OUTCOMES]` | 3-5 outcomes from folder purpose | "Automatically generate production-ready AGENTS.md files for any folder" |
| `[TIER_X_FILES]` | List of files for each tier | "README.md (~1864 words) - Main overview" |
| `[MAX_TOKENS]` | Calculate total if all files loaded | "~15,000 tokens" |
| `[SAVINGS_PERCENT]` | Calculate context savings percentage | "85% reduction" |

**How to Extract:**
- **Overview:** Read README or main files, extract 2-3 paragraphs
- **Concepts:** Analyze folder content, identify 3-10 core concepts
- **Outcomes:** Based on folder purpose, determine 3-5 expected outcomes
- **Token Calculations:** Estimate token costs, calculate savings

### Document Guide Placeholders

| Placeholder | Source | Example |
|------------|--------|---------|
| `[FILE_PURPOSE_SHORT]` | Brief purpose (for heading) | "Project Overview" |
| `[CONTAINS]` | List of main content elements | "Mission statement, Success criteria, Quality gates" |
| `[USE_WHEN_SCENARIO]` | Specific scenarios | "Understanding what the SOP does, Defining success criteria" |
| `[KEY_SECTIONS]` | Main sections in file | "Mission Statement, Success Criteria, Constraints" |
| `[TIER_DESCRIPTION]` | Description of tier | "Essential - Load First" |

**How to Extract:**
- **Contains:** Read file content, list main content elements
- **Key Sections:** Read file headings, list main sections
- **Use When:** Based on file content, create specific scenarios
- **CRITICAL:** Must read actual file content, don't assume

---

## Example: Filled-In Section

Here's an example of a filled-in section to guide replacement:

### Example: Contextual Snippet

**Before (Placeholder):**
```yaml
contextual_snippets:
  - snippet: "[FILE_PURPOSE - first sentence or summary from file]"
    keywords: [KEYWORDS - array of 3-10 relevant keywords from file]
    file: [FILE_NAME]
    tier: [TIER_ASSIGNMENT - 1, 2, or 3]
```

**After (Filled):**
```yaml
contextual_snippets:
  - snippet: "Complete Standard Operating Procedure for automatically generating production-ready AGENTS.md files with progressive context loading for any folder"
    keywords: [sop, agents.md, generation, progressive context loading, automation, folder analysis]
    file: README.md
    tier: 1
```

### Example: Document Guide Section

**Before (Placeholder):**
```markdown
### 1. **[FILE_NAME]** — [FILE_PURPOSE_SHORT]

**Purpose:** [FILE_PURPOSE - full purpose statement]

**Contains:**
- [CONTAINS_ITEM_1 - main content element]
- [CONTAINS_ITEM_2 - another content element]

**Use When:**
- [USE_WHEN_SCENARIO_1 - specific scenario]
- [USE_WHEN_SCENARIO_2 - another scenario]

**Key Sections:**
- [KEY_SECTION_1 - main section name]
- [KEY_SECTION_2 - another section]
```

**After (Filled):**
```markdown
### 1. **README.md** — Project Overview

**Purpose:** Overview and quick start guide for the entire SOP - explains what the tool does, how to use it, and where to start

**Contains:**
- Framework overview and purpose
- Quick start instructions (5 minutes)
- File structure documentation
- Document guide for each file
- Execution workflow diagram
- Success criteria and key principles

**Use When:**
- First time using the tool
- Need orientation and understanding of package contents
- Want quick start instructions
- Need overview of framework structure

**Key Sections:**
- Overview
- Quick Start (5 Minutes)
- File Structure
- Document Guide
- Execution Workflow
- Success Criteria
- Key Principles
```

---

## Notes for AI/LLM Agents

**CRITICAL REQUIREMENTS:**
- ✅ Read actual file contents (don't rely on assumptions)
- ✅ Replace all placeholders systematically (one by one)
- ✅ Verify content matches actual files
- ✅ Use specific purposes (not "Documentation")
- ✅ Create scenario-based use_when statements
- ✅ Validate before delivery

**CONTENT QUALITY:**
- Snippets must match actual file content
- File purposes must be specific and actionable
- Document Guide must list actual sections from files
- Overview must come from actual README
- Key concepts must be specific to folder content

**VALIDATION:**
- Check for remaining placeholders (search for `[`)
- Verify YAML syntax
- Verify all required sections present
- Verify tier assignments are logical
- Verify content quality

---

**End of Framework Definition**

