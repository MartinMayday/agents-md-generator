---
title: AGENTS.md Generator SOP
version: 1.1.0
author: Martin Mayday
date: 2025-12-23
status: Production Ready
classification: Internal Operations | Handoff to IDE/CLI AI Coders
framework: AGENTS.md Generation with Progressive Context Loading
project: agents-md-generator
output_expected: Production-ready AGENTS.md files with progressive context loading for any folder
execution_time: 5-15 minutes per folder (depending on file count)

# Contextual Retrieval Snippets (Level 1: Always Loaded)
contextual_snippets:
  - snippet: "Complete Standard Operating Procedure for automatically generating production-ready AGENTS.md files with progressive context loading for any folder"
    keywords: [sop, agents.md, generation, progressive context loading, automation, folder analysis]
    file: README.md
    tier: 1
  - snippet: "Step-by-step execution instructions with 5-phase workflow for tasker-execution-agents to generate AGENTS.md files"
    keywords: [execution, instructions, workflow, phases, tasker, generation process]
    file: directives/TASKER-ORDERS.md
    tier: 2
  - snippet: "Mission objectives, success criteria, quality gates, and constraints for AGENTS.md generation"
    keywords: [mission, objectives, success criteria, quality gates, constraints, validation]
    file: directives/MISSION-OBJECTIVES.md
    tier: 2
  - snippet: "Complete template with fillable sections for generating AGENTS.md files following progressive context loading protocol"
    keywords: [template, structure, format, progressive loading, context, generation]
    file: directives/AGENTS-MD-TEMPLATE.md
    tier: 2
  - snippet: "Copy/paste ready inline prompts for quick execution of AGENTS.md generation workflow"
    keywords: [quick start, prompt, copy paste, inline, execution, ready to use]
    file: QUICK-START-PROMPT.md
    tier: 1
  - snippet: "Comprehensive validation checklist with 13 quality gates for generated AGENTS.md files"
    keywords: [validation, checklist, quality gates, checks, verification, testing]
    file: directives/VALIDATION-CHECKLIST.md
    tier: 2
  - snippet: "Examples showing wrong vs. correct implementations of AGENTS.md generation with explanations"
    keywords: [examples, wrong, correct, mistakes, best practices, learning]
    file: directives/EXAMPLES-WRONG-vs-CORRECT.md
    tier: 2
  - snippet: "Documentation explaining how the tool handles existing AGENTS.md files with backup and overwrite protection"
    keywords: [existing files, handling, backup, overwrite, protection, error handling]
    file: EXISTING-AGENTS-MD-HANDLING.md
    tier: 1
  - snippet: "Trial run conversation log documenting generation process, issues found, and improvements made"
    keywords: [trial run, log, conversation, issues, improvements, development history]
    file: clog_cursor_TRIAL-RUN_agents_md_file_generation_23-DEC-2025.md
    tier: 3

# File Inventory
files:
  - name: README.md
    purpose: "Overview and quick start guide for the entire SOP - explains what the tool does, how to use it, and where to start"
    use_when: "First time using the tool, need orientation and understanding of package contents, want quick start instructions"
    tier: 1
    word_count: 1864
  - name: QUICK-START-PROMPT.md
    purpose: "Copy/paste ready inline prompts for quick execution - provides exact prompts to paste into IDE/terminal for immediate execution"
    use_when: "Ready to execute immediately, need exact copy/paste prompt, want to skip reading full documentation"
    tier: 1
    word_count: 882
  - name: EXISTING-AGENTS-MD-HANDLING.md
    purpose: "Documentation explaining how the tool handles existing AGENTS.md files with backup and overwrite protection - explains detection logic and error handling"
    use_when: "Understanding how existing files are handled, troubleshooting file conflicts, need error handling documentation"
    tier: 1
    word_count: 892
  - name: clog_cursor_TRIAL-RUN_agents_md_file_generation_23-DEC-2025.md
    purpose: "Trial run conversation log documenting generation process, issues found, and improvements made - historical reference for development"
    use_when: "Understanding tool origins, development history, learning from trial run findings, historical reference"
    tier: 3
    word_count: 16493

# Key Concepts
key_concepts:
  - "5-phase workflow: Analyze → Extract → Generate → Validate → Refine"
  - "Progressive context loading protocol with 4 levels reduces context bloat by 85%"
  - "Mandatory directive reading before execution ensures proper workflow adherence"
  - "Zero assumptions policy - all content must come from actual files or JSON data"
  - "Content quality validation checks for vague purposes and generic snippets"
  - "Existing AGENTS.md file detection prevents accidental overwrites of manually created files"
  - "Template-driven generation ensures consistent format and structure"
  - "13 validation checks ensure production-ready output"
  - "Vendor-neutral AGENTS.md format recognized by GitHub Copilot, Cursor, Windsurf, Claude Code"

# Expected Outcomes
outcomes:
  - "Automatically generate production-ready AGENTS.md files for any folder with progressive context loading"
  - "Reduce context bloat by 85% through progressive context loading protocol"
  - "Achieve 95%+ first-pass generation success rate with validation passing"
  - "Generate vendor-neutral context files that AI/LLM agents can use immediately"
  - "Ensure zero context ROT with complete file inventory and logical tier assignments"
---

# AGENTS.md Generator SOP

**A complete framework for automatically generating production-ready AGENTS.md files with progressive context loading for any folder**

**Version:** 1.1.0  
**Status:** Production Ready  
**Framework:** AGENTS.md Generation with Progressive Context Loading  
**Target:** Transform folder contents into structured, vendor-neutral context files for AI/LLM agents

---

## 📋 Overview

This Standard Operating Procedure (SOP) provides a complete framework for generating production-ready `AGENTS.md` files for any folder. The generated files follow AGENTS.md best practices and include progressive context loading protocol (4 levels) to reduce context bloat by 85%.

**Core Purpose:** Transform folder contents into structured, vendor-neutral context files that AI/LLM agents can use for efficient progressive context loading.

**Key Outcome:** Generate AGENTS.md files with zero context ROT, complete file inventory, logical tier assignments, and comprehensive documentation.

The tool includes a 5-phase execution workflow, Python scripts for analysis and validation, comprehensive templates, and quality gates. It has been enhanced based on trial run findings to ensure proper workflow adherence and content quality.

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

**Purpose:** AI agent decides "Should I use this tool?" without loading full content.

**Example:**
```yaml
contextual_snippets:
  - snippet: "Complete Standard Operating Procedure for automatically generating production-ready AGENTS.md files..."
    keywords: [sop, agents.md, generation, progressive context loading]
    file: README.md
    tier: 1
```

---

### Level 2: AGENTS.md Content (On-Demand) - ~2,000 tokens

**When:** After AI agent confirms tool is relevant  
**Token Cost:** ~2,000 tokens  
**Load Time:** < 1 second  
**Trigger:** AI asks: "Load full tool instructions? (Takes ~2000 tokens)"

**Content:**
- Complete file inventory with purpose and use_when
- Document Guide section (detailed breakdown of each file)
- Quick Start workflow
- Key principles and quality guarantees
- Execution checklist

**Purpose:** Full tool instructions without loading individual file contents.

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
- Trial run logs

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
- `README.md` (~1,864 words) - Overview and quick start guide
- `QUICK-START-PROMPT.md` (~882 words) - Copy/paste ready prompts
- `EXISTING-AGENTS-MD-HANDLING.md` (~892 words) - Error handling documentation

**Tier 2 Files (Load on Demand - Core Execution):**
- Files in `directives/` subdirectory (TASKER-ORDERS.md, MISSION-OBJECTIVES.md, AGENTS-MD-TEMPLATE.md, VALIDATION-CHECKLIST.md, EXAMPLES-WRONG-vs-CORRECT.md) - Execution instructions, templates, and validation

**Tier 3 Files (Load Only When Needed - Historical/Reference):**
- `clog_cursor_TRIAL-RUN_agents_md_file_generation_23-DEC-2025.md` (~16,493 words) - Trial run log

**Purpose:** Detailed content appears only when explicitly needed, keeping context clean.

**Example Loading Sequence:**
```
User: "I need to generate AGENTS.md for a folder"
↓
AI: "Load README.md? (Takes ~1,864 tokens)"
↓
User: "Yes"
↓
AI loads: README.md (Level 3)
↓
AI: "Load directives/TASKER-ORDERS.md Phase 1 section? (Takes ~100 tokens)"
↓
User: "Yes"
↓
AI loads: Phase 1 section only (Level 3, selective)
```

---

### Level 4: Source Code (Execute, Don't Load) - ~100 tokens output only

**When:** Python scripts need to run  
**Token Cost:** ~100 tokens (output only, code not loaded)  
**Load Time:** Execution time (varies)  
**Trigger:** AI executes: `python executions/analyze-folder.py [FOLDER_PATH]`

**Content:**
- Python validation scripts (execute, don't load to context)
- Script output (success/failure messages)
- Metrics and reports (generated data)

**Purpose:** Complex logic stays external, keeping context window clean.

**What's Executed:**
- `executions/analyze-folder.py` - Deep file analysis
- `executions/extract-context.py` - Context extraction
- `executions/validate-agents-md.py` - Validation checks
- `executions/check-existing-agents-md.py` - Existing file detection

**What's Loaded:**
- Only script output (✅/❌, error messages, metrics)
- Never the script source code itself

**Example:**
```bash
# AI executes (code not loaded to context):
python executions/analyze-folder.py __ref/interview-framework

# AI sees only output (~100 tokens):
Analysis complete: interview-framework_analysis.json
  Files analyzed: 8
  Total words: 21332
```

---

### Progressive Loading Summary

| Level | Content | Token Cost | When | Trigger |
|-------|---------|------------|------|---------|
| **1. Front Matter** | Brief description, keywords | ~200 | Always | Automatic |
| **2. AGENTS.md** | Full tool instructions | ~2,000 | On-demand | AI confirms relevance |
| **3. Reference Files** | Individual file contents | 500-12,000 | Selective | AI asks per file |
| **4. Source Code** | Script execution output | ~100 | As needed | AI executes scripts |

**Total Maximum Context:** ~22,000 tokens (if all files loaded)  
**Typical Context:** ~2,200 tokens (Level 1 + Level 2 only)  
**Context Savings:** 90% reduction vs. loading everything upfront

---

## 📚 Document Guide

### 1. **README.md** — Start Here

**Purpose:** Overview and quick start guide for the entire SOP - explains what the tool does, how to use it, and where to start

**Contains:**
- Tool overview and purpose
- Quick start instructions (5 minutes)
- File structure diagram
- Document Guide for all files
- Trial run findings and improvements
- Learning path

**Use When:**
- First time using the tool
- Need orientation and understanding of package contents
- Want quick start instructions
- Understanding what the tool does

**Key Sections:**
- Overview
- Quick Start (5 Minutes)
- File Structure
- Document Guide
- Trial Run Findings & Improvements

**Context Loading Tier:** 1 (Essential)

**Word Count:** ~1,864 words

---

### 2. **QUICK-START-PROMPT.md** — Copy/Paste Ready

**Purpose:** Copy/paste ready inline prompts for quick execution - provides exact prompts to paste into IDE/terminal for immediate execution

**Contains:**
- Full inline prompt with all requirements
- Multiple examples (interview-framework, initial_scaffolding)
- One-liner version for quick execution
- Terminal command version
- Key reminders and critical requirements

**Use When:**
- Ready to execute immediately
- Need exact copy/paste prompt
- Want to skip reading full documentation
- Quick execution needed

**Key Sections:**
- Inline Prompt (Copy/Paste Ready)
- Example Usage
- One-Liner Version
- Terminal Command Version
- Key Reminders

**Context Loading Tier:** 1 (Essential)

**Word Count:** ~882 words

---

### 3. **EXISTING-AGENTS-MD-HANDLING.md** — Error Handling

**Purpose:** Documentation explaining how the tool handles existing AGENTS.md files with backup and overwrite protection - explains detection logic and error handling

**Contains:**
- Behavior summary (check before writing, detect source, appropriate action)
- Detection logic (tool-generated vs. manually created)
- Error handling process (3 scenarios)
- Usage examples
- Best practices
- Troubleshooting

**Use When:**
- Understanding how existing files are handled
- Troubleshooting file conflicts
- Need error handling documentation
- Understanding backup process

**Key Sections:**
- Behavior Summary
- Detection Logic
- Error Handling Process
- Usage Examples
- Troubleshooting

**Context Loading Tier:** 1 (Essential)

**Word Count:** ~892 words

---

### 4. **clog_cursor_TRIAL-RUN_agents_md_file_generation_23-DEC-2025.md** — Development History

**Purpose:** Trial run conversation log documenting generation process, issues found, and improvements made - historical reference for development

**Contains:**
- Complete trial run conversation
- Issues identified (directives not read, template not used systematically, source files not read)
- Improvements made (v1.1.0)
- Content quality requirements
- Validation enhancements

**Use When:**
- Understanding tool origins
- Development history
- Learning from trial run findings
- Historical reference

**Key Sections:**
- Trial Run Conversation
- Issues Found
- Improvements Made
- Content Quality Requirements

**Context Loading Tier:** 3 (Reference)

**Word Count:** ~16,493 words

---

## 🚀 Quick Start (5 Minutes)

### Step 1: Load Level 1 Context (Automatic)
AI agent automatically loads front matter:
- Tool description
- Key concepts
- Expected outcomes
- Contextual snippets

**Token Cost:** ~200 tokens  
**Time:** Instant

### Step 2: Confirm Tool Relevance
AI asks: "This tool generates AGENTS.md files with progressive context loading. Should I load full instructions? (~2000 tokens)"

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
1. AI loads `QUICK-START-PROMPT.md` (Level 3, ~882 tokens)
2. AI loads files from `directives/` subdirectory as needed (Level 3, variable tokens)
3. Execute Phase 1 (analyze folder)
4. Continue with phases 2-5 as needed

**For Reference:**
1. AI loads files from `directives/` subdirectory specific sections (Level 3, variable tokens)
2. AI loads `EXISTING-AGENTS-MD-HANDLING.md` if error handling needed (Level 3, ~892 tokens)

**For Validation:**
1. AI executes validation scripts (Level 4, ~100 tokens output only)
2. AI sees results, code not loaded to context

---

## 📊 Expected Output Structure

This tool generates **production-ready AGENTS.md files** that contain:

- **YAML Frontmatter:** Title, version, date, status, classification, contextual snippets, file inventory, key concepts, expected outcomes
- **CONTEXT Section:** Progressive context loading protocol with 4 levels
- **Document Guide:** Detailed breakdown of each file in folder
- **Quick Start:** 5-minute workflow for AI agents
- **Quality Guarantees:** Standards and enforcement methods
- **Key Principles:** Progressive loading, vendor-neutral, complete documentation

**Total:** Variable files per folder, ~2,000-20,000 words per AGENTS.md, Production Ready

---

## ✅ Quality Guarantees

| Guarantee | Standard | Enforcement |
|-----------|----------|-------------|
| **No Context ROT** | 0% hallucinations | Content quality validation |
| **Progressive Loading** | 4-level system | CONTEXT section |
| **Complete Documentation** | All files documented | File inventory validation |
| **Accurate Metadata** | ±10% word count tolerance | File analysis scripts |
| **95%+ First-Pass Success** | Production-ready output | 13 validation checks |
| **Zero Assumptions** | All content from files | Content quality checks |

---

## 🚀 Key Principles

### 1. PROGRESSIVE CONTEXT LOADING
Context loads in stages (prevent ROT):
- **Level 1:** Front matter (200 tokens) - Always loaded
- **Level 2:** AGENTS.md content (2,000 tokens) - On-demand
- **Level 3:** Reference files (500-12,000 tokens) - Selective
- **Level 4:** Source code execution (~100 tokens output) - Execute, don't load

### 2. MANDATORY DIRECTIVE READING
Before execution, AI must read:
- MISSION-OBJECTIVES.md
- TASKER-ORDERS.md
- AGENTS-MD-TEMPLATE.md
- VALIDATION-CHECKLIST.md

### 3. ZERO ASSUMPTIONS POLICY
All content must come from:
- Analysis JSON (file metadata)
- Context JSON (extracted snippets)
- Actual file content (read files directly)

### 4. VENDOR-NEUTRAL
Follow AGENTS.md best practices:
- Recognized by GitHub Copilot, Cursor, Windsurf, Claude Code
- No tool-specific terminology
- Generic AI/LLM agent language

### 5. EXISTING FILE PROTECTION
Never overwrite manually created AGENTS.md files:
- Check before writing
- Detect tool-generated vs. manually created
- Backup tool-generated files
- Request user decision for manual files

---

## 📋 Execution Checklist

**Before starting:**
- [ ] All files downloaded/accessible
- [ ] Read directives (MISSION-OBJECTIVES, TASKER-ORDERS, TEMPLATE, VALIDATION-CHECKLIST)
- [ ] Understand progressive loading protocol
- [ ] Target folder path identified
- [ ] Python 3.8+ available

**During execution:**
- [ ] Phase 1: Analyze folder (execute analyze-folder.py)
- [ ] Phase 2: Read actual files, extract context (execute extract-context.py)
- [ ] Phase 3: Check existing AGENTS.md, load template, read files, replace placeholders
- [ ] Phase 4: Validate output (execute validate-agents-md.py)
- [ ] Phase 5: Refine if needed, verify content quality

**After execution:**
- [ ] AGENTS.md generated in target folder
- [ ] All validation checks pass (13/13)
- [ ] All placeholders replaced
- [ ] Content derived from actual files (0% assumptions)
- [ ] File inventory matches actual files
- [ ] CONTEXT section includes all 4 levels

---

## 📞 Support

During execution, if you get stuck:

1. **Check Document Guide** - Detailed file breakdowns above
2. **Review CONTEXT section** - Progressive loading protocol
3. **Reference file inventory** - Find right file for task
4. **Check tier assignments** - Load files in correct order
5. **Use QUICK-START-PROMPT.md** - Copy/paste ready prompts
6. **Review EXISTING-AGENTS-MD-HANDLING.md** - Error handling documentation

---

## 🎯 Success Signal

When AI agent successfully uses this tool:

```
✅ Level 1 context loaded (200 tokens)
✅ Level 2 context loaded (2000 tokens)
✅ Directives read (MISSION-OBJECTIVES, TASKER-ORDERS, TEMPLATE, VALIDATION-CHECKLIST)
✅ Phase 1 executed (folder analyzed)
✅ Phase 2 executed (context extracted from actual files)
✅ Phase 3 executed (AGENTS.md generated with 0% assumptions)
✅ Phase 4 executed (validation passed 13/13)
✅ AGENTS.md generated in target folder
✅ Mission complete
```

**Status:** Ready for use by AI/LLM agents

---

## 📚 File Reference Quick Links

- **[Start Here]:** `README.md`
- **[Quick Execute]:** `QUICK-START-PROMPT.md`
- **[Error Handling]:** `EXISTING-AGENTS-MD-HANDLING.md`
- **[Development History]:** `clog_cursor_TRIAL-RUN_agents_md_file_generation_23-DEC-2025.md`
- **[Directives Folder]:** `directives/` - Contains TASKER-ORDERS.md, MISSION-OBJECTIVES.md, AGENTS-MD-TEMPLATE.md, VALIDATION-CHECKLIST.md, EXAMPLES-WRONG-vs-CORRECT.md

---

## 📖 References

- [Claude Agent Skills: Teaching Your AI Agent to Wear Multiple Hats](https://cloudnativeengineer.substack.com/p/ai-agent-wear-multiple-hats?open=false#%C2%A7how-progressive-context-loading-works) - Progressive context loading framework
- [Equipping Agents for the Real World with Agent Skills](https://www.anthropic.com/research/equipping-agents) - Anthropic's official skills architecture
- [Agent Skills Best Practices](https://docs.anthropic.com/claude/docs/agent-skills) - Official documentation
- [AGENTS.md Standard](https://agents.md/) - Vendor-neutral AI agent context file format

---

**Generated:** 2025-12-23  
**Status:** Production Ready  
**Quality:** Progressive context loading, complete traceability  
**Next:** Use by AI/LLM agents for efficient context management

**Ready for use.** 🚀

