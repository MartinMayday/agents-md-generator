# Cursor Slash Command: /generate-agents-md (Universal)

**Version:** 2.0.0  
**Date:** 2025-12-23  
**Status:** Production Ready  
**Platform:** Cursor IDE/CLI  
**Portability:** Works in any repository

---

## Command Definition

Add this section to your project root `AGENTS.md` file (or create one if it doesn't exist):

```markdown
## Custom Commands

### /generate-agents-md

Generate AGENTS.md for a target folder using the agents-md-generator SOP.

**Usage:** `/generate-agents-md [FOLDER_PATH]`

**Description:**
Automatically generates production-ready AGENTS.md files for any folder following the 5-phase workflow defined in the agents-md-generator SOP. The generated file includes progressive context loading protocol (4 levels) and comprehensive validation.

**SOP Source:** Automatically fetches from GitHub (or uses local files if available)

**Parameters:**
- `FOLDER_PATH` (required): Path to target folder containing markdown files
  - Examples: `docs`, `src`, `packages/my-package`

**Workflow:**
1. **PRE-FLIGHT (MANDATORY):**
   - **Smart Source Detection:** Check for local SOP files first, then fetch from GitHub if not found
   - Fetch/Read `MISSION-OBJECTIVES.md` from SOP source
   - Fetch/Read `TASKER-ORDERS.md` from SOP source
   - Fetch/Read `AGENTS-MD-TEMPLATE.md` from SOP source
   - Fetch/Read `VALIDATION-CHECKLIST.md` from SOP source
   - Verify understanding of 5-phase workflow before proceeding

2. **PHASE 1: Analyze Target Folder**
   - Download `analyze-folder.py` script to temp directory (if not local)
   - Execute: `python [TEMP_DIR]/analyze-folder.py [FOLDER_PATH]`
   - Verify: `[FOLDER_NAME]_analysis.json` created successfully
   - Check: All markdown files in folder are listed in analysis

3. **PHASE 2: Extract Context from Files**
   - **CRITICAL:** Read at least first 500 words of EACH markdown file in target folder
   - Extract snippets from ACTUAL file content (not assumptions)
   - Download `extract-context.py` script to temp directory (if not local)
   - Execute: `python [TEMP_DIR]/extract-context.py [FOLDER_PATH] [FOLDER_NAME]_analysis.json`
   - Verify: `[FOLDER_NAME]_context.json` created successfully
   - Verify: Snippets match actual file content

4. **PHASE 3: Generate AGENTS.md Using Template**
   - **CRITICAL:** Check for existing AGENTS.md first
     * Download `check-existing-agents-md.py` script to temp directory (if not local)
     * Execute: `python [TEMP_DIR]/check-existing-agents-md.py [FOLDER_PATH]`
     * If exists and manually created: **STOP** - Report error, request user decision
     * If exists and tool-generated: Backup existing file (`AGENTS.md.backup.[timestamp]`), then proceed
     * If not exists: Proceed normally
   - **CRITICAL:** Load template file completely (fetch from SOP source)
   - **CRITICAL:** Read actual source files (at least first 1000 words of each for Document Guide)
   - Systematically replace ALL placeholders line-by-line:
     * `[FOLDER_TITLE]` → From folder name or README (READ the README)
     * `[FOLDER_DESCRIPTION]` → From folder analysis AND actual README content
     * `[FILE_PURPOSE]` → From context JSON (verify matches actual file content)
     * `[CONTAINS]` → Extract from ACTUAL file content (read files, list sections)
     * `[KEY_SECTIONS]` → Extract from ACTUAL file headings (read files)
     * All other placeholders → Fill from JSON or actual files
   - **ZERO assumptions:** All content must come from JSON data or actual file content
   - Write to: `[FOLDER_PATH]/AGENTS.md`

5. **PHASE 4: Validate Generated AGENTS.md**
   - Download `validate-agents-md.py` script to temp directory (if not local)
   - Execute: `python [TEMP_DIR]/validate-agents-md.py [FOLDER_PATH]/AGENTS.md [FOLDER_PATH]`
   - Verify: All validation checks pass (exit code 0)
   - Check: Validation report shows 13/13 checks passed

6. **PHASE 5: Refine if Needed**
   - If validation fails: Fix issues, re-validate (max 3 iterations)
   - If validation passes: Verify content quality manually:
     * Snippets match actual file content (read files to verify)
     * File purposes are specific (not "Documentation")
     * Document Guide sections match actual files (read files)
     * No assumptions in content
   - **Cleanup:** Remove temp directory and downloaded scripts

**SOP Source Configuration:**
```yaml
sop_source:
  # Primary: GitHub repository (works in any repo)
  github:
    user: "[GITHUB_USER]"  # e.g., "your-username"
    repo: "agents-md-generator"  # Repository name
    branch: "main"  # or specific tag/commit
    base_url: "https://raw.githubusercontent.com/{user}/{repo}/{branch}/"
  
  # Fallback: Local files (if SOP is in this repo)
  local:
    base_path: "__ref/SOPs/agents-md-generator"  # Optional: if SOP files exist locally
  
  # Alternative: Custom URL (for self-hosted)
  custom:
    base_url: ""  # Optional: custom base URL
```

**Smart Source Detection Logic:**
1. **Check local files first** (if `local.base_path` exists and contains SOP files)
2. **Fallback to GitHub** (if local not found, use GitHub raw URLs)
3. **Fallback to custom URL** (if GitHub unavailable, use custom URL)
4. **Error if all fail** (report error, cannot proceed)

**File Fetching:**
- **Directives:** Fetch from `{base_url}directives/{filename}.md`
- **Scripts:** Download from `{base_url}executions/{script}.py` to temp directory
- **Use web scraping tools:** Firecrawl MCP, Tavily MCP, or Browser MCP to fetch URLs

**Success Criteria:**
- ✅ AGENTS.md generated in target folder
- ✅ All validation checks pass (13/13)
- ✅ All placeholders replaced
- ✅ Content derived from actual files (0% assumptions)
- ✅ File inventory matches actual files
- ✅ CONTEXT section includes all 4 levels
- ✅ Temp files cleaned up

**Requirements:**
- Python 3.8+ available
- Target folder path accessible
- Target folder contains at least one markdown file
- Internet access (for GitHub fetch) OR local SOP files present
- Web scraping capability (Firecrawl/Tavily/Browser MCP) for fetching URLs

**Error Handling:**
- If folder not found: Report error, exit
- If no markdown files: Report warning, ask user to confirm
- If SOP source unavailable: Report error, suggest local installation or check internet
- If existing AGENTS.md is manually created: STOP, request user decision
- If validation fails: Report which checks failed, allow refinement (max 3 iterations)
- If temp directory creation fails: Report error, exit

**Examples:**
```
/generate-agents-md docs
/generate-agents-md src
/generate-agents-md packages/my-package
```

**Output:**
- `AGENTS.md` file in target folder
- `[FOLDER_NAME]_analysis.json` (temporary, can be cleaned up)
- `[FOLDER_NAME]_context.json` (temporary, can be cleaned up)
- Validation report (stdout)
- Temp directory removed after execution

**Notes:**
- Follows agents-md-generator SOP v1.1.0
- Implements progressive context loading protocol (4 levels)
- Zero assumptions policy enforced
- Content quality validation included
- Works in any repository (no local SOP files required)
- Automatically fetches SOP files from GitHub
- Smart fallback to local files if available
```

---

## Configuration

### Option 1: Default GitHub Repository (Recommended)

Use the default GitHub repository hosting the SOP:

```yaml
sop_source:
  github:
    user: "your-username"  # Replace with actual GitHub username
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
    branch: "main"  # or "v1.1.0" for specific version
```

### Option 3: Local Files (If SOP in Repo)

If the SOP files exist in this repository:

```yaml
sop_source:
  local:
    base_path: "__ref/SOPs/agents-md-generator"
```

### Option 4: Custom URL (Self-Hosted)

Use a custom URL for self-hosted SOP files:

```yaml
sop_source:
  custom:
    base_url: "https://your-domain.com/agents-md-generator/"
```

---

## Installation Instructions

### Step 1: Add to Project Root AGENTS.md

1. Open or create `AGENTS.md` in your project root directory
2. Add the command definition above to the file
3. **Configure SOP source** (choose one of the options above)
4. Save the file

### Step 2: Verify Requirements

Ensure:
- Python 3.8+ is installed and accessible
- Internet access (for GitHub fetch) OR local SOP files present
- Web scraping tools available (Firecrawl/Tavily/Browser MCP) in Cursor

### Step 3: Test Command

1. Open Cursor IDE
2. Type `/generate-agents-md` in the chat
3. Follow the prompt to provide folder path
4. Verify command executes successfully

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
**Solution:** Ensure AGENTS.md is in project root and contains the command definition

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

## Advanced Configuration

### Using Specific Version/Tag

Pin to a specific version for stability:

```yaml
sop_source:
  github:
    user: "your-username"
    repo: "agents-md-generator"
    branch: "v1.1.0"  # Use specific tag
```

### Using Custom Branch

Use a development or feature branch:

```yaml
sop_source:
  github:
    user: "your-username"
    repo: "agents-md-generator"
    branch: "feature/new-feature"  # Use specific branch
```

### Hybrid: Local + GitHub Fallback

Use local files if available, fallback to GitHub:

```yaml
sop_source:
  local:
    base_path: "__ref/SOPs/agents-md-generator"  # Check first
  github:
    user: "your-username"
    repo: "agents-md-generator"
    branch: "main"  # Fallback if local not found
```

---

**Version:** 2.0.0  
**Last Updated:** 2025-12-23  
**Status:** Production Ready  
**Compatible with:** Cursor IDE/CLI  
**Portability:** Works in any repository

