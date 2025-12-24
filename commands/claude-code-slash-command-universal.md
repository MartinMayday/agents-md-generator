# Claude Code Slash Command: /generate-agents-md (Universal)

**Version:** 2.0.0  
**Date:** 2025-12-23  
**Status:** Production Ready  
**Platform:** Claude Code IDE/CLI  
**Portability:** Works in any repository

---

## File Location

Create this file at:
```
.claude/commands/generate-agents-md.md
```

---

## Command Definition

```markdown
# /generate-agents-md

Generate AGENTS.md for a target folder using the agents-md-generator SOP.

## Usage

```
/generate-agents-md [FOLDER_PATH]
```

## Description

Automatically generates production-ready AGENTS.md files for any folder following the 5-phase workflow defined in the agents-md-generator SOP. The generated file includes progressive context loading protocol (4 levels) and comprehensive validation.

**SOP Source:** Automatically fetches from GitHub (or uses local files if available)

## Parameters

- **FOLDER_PATH** (required): Path to target folder containing markdown files
  - Examples: `docs`, `src`, `packages/my-package`
  - Can be relative to project root or absolute path

## SOP Source Configuration

The command automatically detects and uses the best available SOP source:

1. **Local Files** (if SOP exists in this repository)
   - Path: `__ref/SOPs/agents-md-generator/` (or configured path)
   - Checked first for fastest access

2. **GitHub Raw URLs** (primary fallback)
   - Repository: `https://github.com/[USER]/agents-md-generator`
   - Branch: `main` (or configured branch/tag)
   - Base URL: `https://raw.githubusercontent.com/[USER]/agents-md-generator/[BRANCH]/`

3. **Custom URL** (optional fallback)
   - Configured custom base URL for self-hosted SOP files

**Configuration:**
```yaml
# Add to .claude/config.yaml or command file
sop_source:
  github:
    user: "[GITHUB_USER]"  # e.g., "your-username"
    repo: "agents-md-generator"
    branch: "main"  # or specific tag like "v1.1.0"
  local:
    base_path: "__ref/SOPs/agents-md-generator"  # Optional
  custom:
    base_url: ""  # Optional custom URL
```

## Workflow

### PRE-FLIGHT (MANDATORY)

Before starting execution, you MUST:

1. **Detect SOP Source:**
   - Check for local SOP files at configured path
   - If not found, use GitHub raw URLs
   - If GitHub unavailable, try custom URL
   - Report error if all sources unavailable

2. **Fetch/Read Directives:**
   - MISSION-OBJECTIVES.md from SOP source
   - TASKER-ORDERS.md from SOP source
   - AGENTS-MD-TEMPLATE.md from SOP source
   - VALIDATION-CHECKLIST.md from SOP source
   - Use web scraping tools (Firecrawl/Tavily/Browser MCP) if fetching from URLs

3. **Verify understanding** of 5-phase workflow before proceeding

**VERIFICATION:** Confirm you have read all mandatory directives and understand the workflow.

### PHASE 1: Analyze Target Folder

**Objective:** Deep analysis of folder structure and files to extract metadata

**Execution:**
1. Download `analyze-folder.py` script to temp directory (if not local)
2. Execute: `python [TEMP_DIR]/analyze-folder.py [FOLDER_PATH]`

**Expected Output:**
- JSON file: `[FOLDER_NAME]_analysis.json`
- Contains: file metadata, structure, relationships, file types

**Validation:**
- [ ] JSON file created successfully
- [ ] All markdown files in folder are listed
- [ ] File metadata is accurate (size, word count, last modified)

**Error Handling:**
- If folder not found: Report error, exit
- If no markdown files: Report warning, ask user to confirm
- If analysis fails: Report error details, exit

### PHASE 2: Extract Context from Files

**Objective:** Extract contextual snippets, keywords, and determine tier assignments

**CRITICAL: MUST READ ACTUAL FILE CONTENTS**

Before running extraction script, you MUST:
1. Read at least the first 500 words of EACH markdown file in target folder
2. Extract actual snippets from file content (not from assumptions)
3. Verify snippets match actual file content

**Execution:**
1. Download `extract-context.py` script to temp directory (if not local)
2. Execute: `python [TEMP_DIR]/extract-context.py [FOLDER_PATH] [FOLDER_NAME]_analysis.json`

**Expected Output:**
- JSON file: `[FOLDER_NAME]_context.json`
- Contains: contextual snippets, keywords, tier assignments, file purposes, use_when statements

**Content Source Verification:**
- [ ] Snippets extracted from actual file content (read files, not assumptions)
- [ ] Keywords extracted from file content (frontmatter, headings, text)
- [ ] File purposes derived from actual file content (not generic descriptions)
- [ ] use_when statements based on actual file content analysis

**Validation:**
- [ ] JSON file created successfully
- [ ] All files have contextual snippets (Level 1) - VERIFIED from actual content
- [ ] All files have keywords (minimum 3 per file) - EXTRACTED from content
- [ ] All files have tier assignments (1, 2, or 3)
- [ ] All files have specific purposes (not vague) - DERIVED from content

### PHASE 3: Generate AGENTS.md Using Template

**Objective:** Generate AGENTS.md file by filling template with extracted data

**CRITICAL: CHECK FOR EXISTING AGENTS.md BEFORE WRITING**

**Pre-Write Check:**
1. Download `check-existing-agents-md.py` script to temp directory (if not local)
2. Execute: `python [TEMP_DIR]/check-existing-agents-md.py [FOLDER_PATH]`
3. Exit code 0 (not exists): Proceed normally
4. Exit code 1 (tool-generated): Backup existing file, proceed with overwrite
5. Exit code 2 (manually created): **STOP** - Report error, request user decision

**CRITICAL: SYSTEMATIC TEMPLATE REPLACEMENT**

You MUST:
1. **Load template file** - Fetch/Read `AGENTS-MD-TEMPLATE.md` from SOP source
2. **Load analysis JSON** - Read `[FOLDER_NAME]_analysis.json`
3. **Load context JSON** - Read `[FOLDER_NAME]_context.json`
4. **Read actual source files** - For Document Guide sections, read actual file content (at least first 1000 words of each file)
5. **Systematically replace placeholders** - Go through template line by line:
   - `[FOLDER_TITLE]` → Extract from folder name or first README (READ the README)
   - `[FOLDER_DESCRIPTION]` → Extract from folder analysis AND actual README content
   - `[KEY_CONCEPTS]` → Extract from context JSON AND verify against actual file content
   - `[FILE_NAME]` → From analysis JSON
   - `[FILE_PURPOSE]` → From context JSON (verify it matches actual file content)
   - `[TIER_ASSIGNMENT]` → From context JSON
   - `[FILE_METADATA]` → From analysis JSON
   - `[CONTAINS]` → Extract from ACTUAL file content (read files, list sections)
   - `[USE_WHEN_SCENARIO]` → Based on ACTUAL file content analysis
   - `[KEY_SECTIONS]` → Extract from ACTUAL file headings (read files)
   - All other placeholders → Fill from appropriate source (JSON or actual files)

**Content Source Requirements:**
- **0% assumptions** - All content must come from:
  - Analysis JSON (file metadata)
  - Context JSON (extracted snippets)
  - Actual file content (read files directly)
- **Document Guide sections** - MUST read actual file content to write "Contains" and "Key Sections"
- **Overview text** - MUST read README or main files to extract actual description

**Process:**
1. Check for existing AGENTS.md (execute check script)
2. If backup needed: Create backup of existing AGENTS.md (rename to `AGENTS.md.backup.[timestamp]`)
3. Load template file (fetch from SOP source, don't rely on memory)
4. Load analysis JSON
5. Load context JSON
6. **Read actual source files** (at least first 1000 words of each for Document Guide)
7. **Systematically replace placeholders** (one by one, verify each replacement)
8. Generate complete AGENTS.md content
9. Write to `[FOLDER_PATH]/AGENTS.md` (only after confirmation if file exists)

**Verification Before Writing:**
- [ ] Existing AGENTS.md checked and handled appropriately
- [ ] All placeholders replaced (search for `[` in output)
- [ ] Document Guide sections based on actual file content (not assumptions)
- [ ] Overview text extracted from actual README/content
- [ ] Key concepts verified against actual file content

### PHASE 4: Validate Generated AGENTS.md

**Objective:** Validate generated AGENTS.md against all requirements

**Execution:**
1. Download `validate-agents-md.py` script to temp directory (if not local)
2. Execute: `python [TEMP_DIR]/validate-agents-md.py [FOLDER_PATH]/AGENTS.md [FOLDER_PATH]`

**Expected Output:**
- Validation report (stdout)
- Exit code: 0 = pass, 1 = fail

**Validation Checks:**
1. YAML frontmatter validity
2. All required sections present
3. CONTEXT section has 4 levels
4. Tier assignments are valid (1, 2, or 3)
5. No placeholder text remains
6. File inventory matches actual files
7. Word counts are reasonable
8. Keywords are relevant
9. Content quality - Snippets match actual file content (not generic)
10. Content quality - File purposes are specific (not vague like "Documentation")
11. Content quality - Document Guide sections reference actual file content

**Error Handling:**
- If validation fails: Report which checks failed, provide details
- If file not found: Report error, exit
- If validation script error: Report error details, exit

**Decision Point:**
- If validation passes (exit code 0) → Proceed to Phase 5
- If validation fails (exit code 1) → Proceed to Phase 5 (refinement)

### PHASE 5: Refine Based on Validation Results

**Objective:** Fix any issues identified during validation

**If Validation Passed:**
- [ ] Review generated AGENTS.md manually
- [ ] **Verify content is from files** - Check snippets match actual file content
- [ ] **Verify file purposes are specific** - Not vague like "Documentation", must be actionable
- [ ] **Verify use_when statements are actionable** - Scenario-based, not "When needed"
- [ ] **Verify tier assignments are logical** - Tier 1=essential, Tier 2=core, Tier 3=reference
- [ ] **Verify Document Guide sections** - "Contains" and "Key Sections" match actual files
- [ ] **Verify no assumptions** - All content traceable to JSON or actual files
- [ ] **Cleanup:** Remove temp directory and downloaded scripts
- [ ] If all checks pass → **MISSION COMPLETE**

**If Validation Failed:**
1. Review validation report
2. Identify failed checks
3. For each failed check:
   - **YAML errors:** Fix syntax, re-validate
   - **Missing sections:** Add missing sections from template
   - **CONTEXT section issues:** Ensure all 4 levels are present
   - **Tier assignment issues:** Review tier logic, adjust assignments
   - **Placeholder text:** Replace remaining placeholders
   - **File inventory mismatches:** Update inventory to match actual files
   - **Word count issues:** Recalculate word counts
   - **Keyword issues:** Re-extract keywords from content
4. Re-run Phase 4 (validation)
5. Repeat until validation passes

**Refinement Limits:**
- Maximum 3 refinement iterations
- If validation still fails after 3 iterations → Report error, request human intervention

## Success Criteria

**Mission is successful when:**

1. ✅ AGENTS.md file generated in target folder
2. ✅ All validation checks pass (exit code 0)
3. ✅ All placeholders replaced
4. ✅ File inventory matches actual files
5. ✅ CONTEXT section includes all 4 levels
6. ✅ Tier assignments are logical
7. ✅ Documentation quality meets standards
8. ✅ Temp files cleaned up

## Requirements

- Python 3.8+ available
- Target folder path accessible
- Target folder contains at least one markdown file
- Internet access (for GitHub fetch) OR local SOP files present
- Web scraping capability (Firecrawl/Tavily/Browser MCP) for fetching URLs

## Error Handling

### Error Type 1: SOP Source Unavailable
**Action:** 
- Check internet connection (for GitHub)
- Verify GitHub repository exists and is accessible
- Check if local SOP files exist (if using local source)
- Report error if all sources unavailable

### Error Type 2: Folder Not Found
**Action:** Verify folder path, check permissions, retry

### Error Type 3: No Markdown Files
**Action:** Report warning, ask user to confirm, proceed with empty inventory

### Error Type 4: Analysis Failure
**Action:** Check file permissions, verify Python version, review error logs

### Error Type 5: Context Extraction Failure
**Action:** Check file encoding, verify file readability, review error logs

### Error Type 6: Template Replacement Failure
**Action:** Verify template format, check JSON structure, review error logs

### Error Type 7: Existing AGENTS.md File
**Action:** 
- If generated by this tool: Backup existing file, proceed with overwrite
- If manually created: Report error, request user decision (backup/abort/merge)
- If user chooses abort: Stop execution
- If user chooses backup: Create backup, proceed with overwrite
- If user chooses merge: Report "Merge not supported yet", request backup/abort

### Error Type 8: Validation Failure
**Action:** Review validation report, fix issues, re-validate (max 3 iterations)

### Error Type 9: Temp Directory Creation Failure
**Action:** Check disk space, verify write permissions, report error

## Examples

### Example 1: Generate for docs folder
```
/generate-agents-md docs
```

### Example 2: Generate for src folder
```
/generate-agents-md src
```

### Example 3: Generate for packages/my-package folder
```
/generate-agents-md packages/my-package
```

## Output

- `AGENTS.md` file in target folder
- `[FOLDER_NAME]_analysis.json` (temporary, can be cleaned up)
- `[FOLDER_NAME]_context.json` (temporary, can be cleaned up)
- Validation report (stdout)
- Temp directory removed after execution

## Notes

- Follows agents-md-generator SOP v1.1.0
- Implements progressive context loading protocol (4 levels)
- Zero assumptions policy enforced
- Content quality validation included
- Works in any repository (no local SOP files required)
- Automatically fetches SOP files from GitHub
- Smart fallback to local files if available
- Cleans up temp files after execution
```

---

## Installation Instructions

### Step 1: Create Commands Directory

```bash
mkdir -p .claude/commands
```

### Step 2: Create Command File

1. Create file: `.claude/commands/generate-agents-md.md`
2. Copy the command definition above into the file
3. **Configure SOP source** (see Configuration section below)
4. Save the file

### Step 3: Configure SOP Source

Add configuration to `.claude/config.yaml` or in the command file:

```yaml
sop_source:
  github:
    user: "your-username"  # Replace with actual GitHub username
    repo: "agents-md-generator"
    branch: "main"  # or "v1.1.0" for specific version
  local:
    base_path: "__ref/SOPs/agents-md-generator"  # Optional: if SOP exists locally
```

### Step 4: Test Command

1. Open Claude Code IDE
2. Type `/generate-agents-md` in the chat
3. Follow the prompt to provide folder path
4. Verify command executes successfully

---

## Configuration Options

### Option 1: Default GitHub Repository

Use the default GitHub repository:

```yaml
sop_source:
  github:
    user: "your-username"
    repo: "agents-md-generator"
    branch: "main"
```

### Option 2: Custom GitHub Repository

Use your own fork or custom repository:

```yaml
sop_source:
  github:
    user: "your-org"
    repo: "your-agents-md-generator"
    branch: "v1.1.0"  # Use specific version tag
```

### Option 3: Local Files Only

If the SOP files exist in this repository:

```yaml
sop_source:
  local:
    base_path: "__ref/SOPs/agents-md-generator"
```

### Option 4: Hybrid (Local + GitHub Fallback)

Use local if available, fallback to GitHub:

```yaml
sop_source:
  local:
    base_path: "__ref/SOPs/agents-md-generator"
  github:
    user: "your-username"
    repo: "agents-md-generator"
    branch: "main"
```

---

## Usage Example

**User Input:**
```
/generate-agents-md docs
```

**Expected Behavior:**
1. AI detects SOP source (GitHub or local)
2. AI fetches/reads all directives from SOP source
3. AI downloads Python scripts to temp directory
4. AI executes Phase 1 (analyze folder)
5. AI executes Phase 2 (extract context)
6. AI generates AGENTS.md using template
7. AI executes Phase 4 (validate)
8. AI cleans up temp files
9. AI reports completion status

**Expected Output:**
```
✅ SOP source detected: GitHub (https://raw.githubusercontent.com/...)
✅ Phase 1: Analysis complete - docs_analysis.json created
✅ Phase 2: Context extraction complete - docs_context.json created
✅ Phase 3: AGENTS.md generated in docs/
✅ Phase 4: Validation passed (13/13 checks)
✅ Phase 5: Content quality verified
✅ Temp files cleaned up
✅ Mission complete: AGENTS.md ready for use
```

---

## Troubleshooting

### Issue: "SOP source unavailable"
**Solution:** 
- Check internet connection (for GitHub)
- Verify GitHub repository exists and is accessible
- Check if local SOP files exist (if using local source)
- Verify custom URL is correct (if using custom source)

### Issue: "Command not recognized"
**Solution:** Ensure `.claude/commands/generate-agents-md.md` exists and contains the command definition

### Issue: "Python not found"
**Solution:** Ensure Python 3.8+ is installed and accessible in PATH

### Issue: "Folder not found"
**Solution:** Verify folder path is correct and accessible from project root

### Issue: "Validation failed"
**Solution:** Review validation report, fix issues, re-run command (max 3 iterations)

### Issue: "Cannot fetch from GitHub"
**Solution:** 
- Check internet connection
- Verify GitHub repository URL is correct
- Try using local files if available
- Check if web scraping tools (Firecrawl/Tavily) are configured

---

**Version:** 2.0.0  
**Last Updated:** 2025-12-23  
**Status:** Production Ready  
**Compatible with:** Claude Code IDE/CLI  
**Portability:** Works in any repository

