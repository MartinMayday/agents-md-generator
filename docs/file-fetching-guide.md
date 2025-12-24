# File Fetching Guide

**Version:** 1.0.0  
**Date:** 2025-12-23  
**Status:** Production Ready  
**Purpose:** Guide for AI agents on fetching directives and downloading scripts from different sources

---

## Overview

This guide documents how AI agents should fetch SOP files (directives and scripts) from different sources (local, GitHub, custom URL). It covers web scraping tools, script downloads, temp directory management, and error handling.

**Key Principle:** Directives are fetched and cached in memory (not written to disk). Scripts are downloaded to temp directory, executed, then cleaned up.

---

## File Types

### Directives (Markdown Files)
- **Purpose:** Configuration and templates for AGENTS.md generation
- **Storage:** Memory only (not written to disk)
- **Files:**
  - `MISSION-OBJECTIVES.md`
  - `TASKER-ORDERS.md`
  - `AGENTS-MD-TEMPLATE.md`
  - `VALIDATION-CHECKLIST.md`
  - `EXAMPLES-WRONG-vs-CORRECT.md` (optional)

### Scripts (Python Files)
- **Purpose:** Execution scripts for analysis and validation
- **Storage:** Temp directory (downloaded, executed, cleaned up)
- **Files:**
  - `analyze-folder.py`
  - `extract-context.py`
  - `validate-agents-md.py`
  - `check-existing-agents-md.py`

---

## Source 1: Local Files

### Fetching Directives

**Method:** Use `read_file` tool directly

**Example:**
```python
# Base path from source detection
base_path = "__ref/SOPs/agents-md-generator"

# Fetch directives
mission_objectives = read_file(f"{base_path}/directives/MISSION-OBJECTIVES.md")
tasker_orders = read_file(f"{base_path}/directives/TASKER-ORDERS.md")
template = read_file(f"{base_path}/directives/AGENTS-MD-TEMPLATE.md")
validation = read_file(f"{base_path}/directives/VALIDATION-CHECKLIST.md")
```

**Advantages:**
- Fastest (no network)
- Works offline
- No authentication needed
- Most reliable

**Error Handling:**
- If file not found: Report error, try fallback source
- If read fails: Report error with file path

### Using Scripts

**Method:** Execute directly from local path

**Example:**
```python
# Execute script directly
run_terminal_cmd(f"python {base_path}/executions/analyze-folder.py {folder_path}")
```

**No download needed** - scripts are already local.

---

## Source 2: GitHub Raw URLs

### Fetching Directives

**Method:** Use web scraping tools (Firecrawl MCP, Tavily MCP, or Browser MCP)

**URL Construction:**
```
{base_url}directives/{filename}.md
```

**Example URLs:**
- `https://raw.githubusercontent.com/user/repo/main/__ref/SOPs/agents-md-generator/directives/MISSION-OBJECTIVES.md`
- `https://raw.githubusercontent.com/user/repo/main/__ref/SOPs/agents-md-generator/directives/TASKER-ORDERS.md`

#### Option A: Firecrawl MCP (Recommended)

**Tool:** `mcp_firecrawl_firecrawl_scrape`

**Example:**
```python
# Fetch directive
url = f"{base_url}directives/MISSION-OBJECTIVES.md"
result = firecrawl_scrape(
    url=url,
    formats=["markdown"],
    onlyMainContent=True
)
mission_objectives = result["markdown"]
```

**Advantages:**
- Reliable markdown extraction
- Handles GitHub raw content well
- Clean output

#### Option B: Tavily MCP

**Tool:** `mcp_tavily-remote-mcp_tavily_extract`

**Example:**
```python
# Fetch directive
url = f"{base_url}directives/MISSION-OBJECTIVES.md"
result = tavily_extract(
    urls=[url],
    format="markdown"
)
mission_objectives = result[0]["content"]
```

**Advantages:**
- Good for multiple URLs
- Can extract from multiple sources

#### Option C: Browser MCP

**Tool:** `mcp_cursor-ide-browser_browser_navigate` + `mcp_cursor-ide-browser_browser_snapshot`

**Example:**
```python
# Navigate to URL
browser_navigate(url=f"{base_url}directives/MISSION-OBJECTIVES.md")

# Get content
snapshot = browser_snapshot()
mission_objectives = extract_markdown_from_snapshot(snapshot)
```

**Advantages:**
- Most flexible
- Can handle complex pages

**Disadvantages:**
- Slower than direct fetch
- More complex

#### Option D: Direct HTTP (Fallback)

**If MCP tools unavailable, use terminal commands:**

```python
# Using curl
result = run_terminal_cmd(f"curl -s {url}")
mission_objectives = result.stdout
```

**Or using Python:**
```python
# Create temporary Python script
script = f"""
import urllib.request
url = "{url}"
response = urllib.request.urlopen(url)
content = response.read().decode('utf-8')
print(content)
"""
run_terminal_cmd(f"python -c '{script}'")
```

### Downloading Scripts

**Method:** Download to temp directory, then execute

**Temp Directory Structure:**
```
{temp_dir}/
└── executions/
    ├── analyze-folder.py
    ├── extract-context.py
    ├── validate-agents-md.py
    └── check-existing-agents-md.py
```

#### Step 1: Create Temp Directory

```python
import tempfile
import os
from datetime import datetime

# Create temp directory
temp_dir = tempfile.mkdtemp(prefix=f"agents-md-generator-{datetime.now().strftime('%Y%m%d-%H%M%S')}-")
executions_dir = os.path.join(temp_dir, "executions")
os.makedirs(executions_dir, exist_ok=True)
```

#### Step 2: Download Scripts

**URL Construction:**
```
{base_url}executions/{script_name}.py
```

**Example URLs:**
- `https://raw.githubusercontent.com/user/repo/main/__ref/SOPs/agents-md-generator/executions/analyze-folder.py`

**Download Methods:**

**Option A: Using curl (Recommended)**
```python
scripts = [
    "analyze-folder.py",
    "extract-context.py",
    "validate-agents-md.py",
    "check-existing-agents-md.py"
]

for script in scripts:
    url = f"{base_url}executions/{script}"
    output_path = os.path.join(executions_dir, script)
    
    # Download
    run_terminal_cmd(f"curl -s -o {output_path} {url}")
    
    # Verify download
    if not os.path.exists(output_path):
        raise Exception(f"Failed to download {script} from {url}")
    
    # Make executable
    os.chmod(output_path, 0o755)
```

**Option B: Using Python urllib**
```python
import urllib.request

for script in scripts:
    url = f"{base_url}executions/{script}"
    output_path = os.path.join(executions_dir, script)
    
    # Download
    urllib.request.urlretrieve(url, output_path)
    
    # Verify download
    if not os.path.exists(output_path):
        raise Exception(f"Failed to download {script} from {url}")
    
    # Make executable
    os.chmod(output_path, 0o755)
```

**Option C: Using wget**
```python
for script in scripts:
    url = f"{base_url}executions/{script}"
    output_path = os.path.join(executions_dir, script)
    
    # Download
    run_terminal_cmd(f"wget -q -O {output_path} {url}")
    
    # Verify download
    if not os.path.exists(output_path):
        raise Exception(f"Failed to download {script} from {url}")
    
    # Make executable
    os.chmod(output_path, 0o755)
```

#### Step 3: Execute Scripts

```python
# Execute script from temp directory
script_path = os.path.join(executions_dir, "analyze-folder.py")
run_terminal_cmd(f"python {script_path} {folder_path}")
```

#### Step 4: Cleanup

```python
import shutil

# Remove temp directory
try:
    shutil.rmtree(temp_dir)
except Exception as e:
    log_warning(f"Failed to cleanup temp directory {temp_dir}: {e}")
```

**Important:** Always cleanup temp directory, even on errors (use try/finally).

---

## Source 3: Custom URL

### Fetching Directives

**Method:** Same as GitHub (web scraping tools or HTTP)

**URL Construction:**
```
{base_url}directives/{filename}.md
```

**Example:**
```python
url = f"{base_url}directives/MISSION-OBJECTIVES.md"
# Use same methods as GitHub (Firecrawl, Tavily, Browser MCP, or curl)
```

### Downloading Scripts

**Method:** Same as GitHub (download to temp directory)

**URL Construction:**
```
{base_url}executions/{script_name}.py
```

**Example:**
```python
url = f"{base_url}executions/analyze-folder.py"
# Use same download methods as GitHub
```

**Note:** Custom URLs may require authentication. Handle authentication if needed (see Advanced section).

---

## Complete Implementation Example

### Fetch All Directives

```python
def fetchDirectives(source_info):
    """
    Fetch all directives from detected source.
    
    Returns:
        dict: Directives with keys: mission_objectives, tasker_orders, template, validation
    """
    directives = {}
    
    if source_info["type"] == "local":
        # Local files
        base_path = source_info["base_path"]
        directives["mission_objectives"] = read_file(f"{base_path}/directives/MISSION-OBJECTIVES.md")
        directives["tasker_orders"] = read_file(f"{base_path}/directives/TASKER-ORDERS.md")
        directives["template"] = read_file(f"{base_path}/directives/AGENTS-MD-TEMPLATE.md")
        directives["validation"] = read_file(f"{base_path}/directives/VALIDATION-CHECKLIST.md")
        
    elif source_info["type"] == "github" or source_info["type"] == "custom":
        # GitHub or custom URL
        base_url = source_info["base_url"]
        
        # Fetch using Firecrawl (or fallback to curl)
        directive_files = [
            "MISSION-OBJECTIVES.md",
            "TASKER-ORDERS.md",
            "AGENTS-MD-TEMPLATE.md",
            "VALIDATION-CHECKLIST.md"
        ]
        
        for filename in directive_files:
            url = f"{base_url}directives/{filename}"
            
            try:
                # Try Firecrawl first
                result = firecrawl_scrape(url=url, formats=["markdown"], onlyMainContent=True)
                content = result["markdown"]
            except:
                # Fallback to curl
                result = run_terminal_cmd(f"curl -s {url}")
                content = result.stdout
            
            # Store in directives dict
            key = filename.replace(".md", "").lower().replace("-", "_")
            directives[key] = content
    
    return directives
```

### Download and Execute Scripts

```python
def downloadAndExecuteScript(source_info, script_name, args):
    """
    Download script from source and execute it.
    
    Returns:
        dict: Execution result with stdout, stderr, exit_code
    """
    import tempfile
    import os
    import shutil
    from datetime import datetime
    
    # Create temp directory
    temp_dir = tempfile.mkdtemp(prefix=f"agents-md-generator-{datetime.now().strftime('%Y%m%d-%H%M%S')}-")
    executions_dir = os.path.join(temp_dir, "executions")
    os.makedirs(executions_dir, exist_ok=True)
    
    try:
        # Download script
        if source_info["type"] == "local":
            # Copy from local
            source_path = f"{source_info['base_path']}/executions/{script_name}"
            dest_path = os.path.join(executions_dir, script_name)
            shutil.copy(source_path, dest_path)
        else:
            # Download from URL
            url = f"{source_info['base_url']}executions/{script_name}"
            dest_path = os.path.join(executions_dir, script_name)
            
            # Download using curl
            run_terminal_cmd(f"curl -s -o {dest_path} {url}")
            
            # Verify download
            if not os.path.exists(dest_path):
                raise Exception(f"Failed to download {script_name} from {url}")
        
        # Make executable
        os.chmod(dest_path, 0o755)
        
        # Execute script
        cmd = f"python {dest_path} {args}"
        result = run_terminal_cmd(cmd)
        
        return {
            "stdout": result.stdout,
            "stderr": result.stderr,
            "exit_code": result.returncode
        }
    
    finally:
        # Always cleanup
        try:
            shutil.rmtree(temp_dir)
        except Exception as e:
            log_warning(f"Failed to cleanup temp directory: {e}")
```

---

## Error Handling

### Directive Fetch Errors

**Error:** File not found (404)
```
Error: Cannot fetch MISSION-OBJECTIVES.md from {url}
Reason: File not found (404)
Solution: Verify URL is correct and file exists in repository
```

**Error:** Network timeout
```
Error: Cannot fetch MISSION-OBJECTIVES.md from {url}
Reason: Network timeout
Solution: Check internet connection, try again
```

**Error:** Authentication required
```
Error: Cannot fetch MISSION-OBJECTIVES.md from {url}
Reason: Authentication required (401/403)
Solution: Configure authentication or use public repository
```

### Script Download Errors

**Error:** Download failed
```
Error: Cannot download analyze-folder.py from {url}
Reason: {error_message}
Solution: Verify URL is correct, check internet connection
```

**Error:** Script not executable
```
Error: Script analyze-folder.py is not executable
Reason: File permissions issue
Solution: Check file permissions, make executable
```

**Error:** Script execution failed
```
Error: Script analyze-folder.py exited with code {exit_code}
Reason: {error_message}
Solution: Check script output for details
```

### Temp Directory Errors

**Error:** Cannot create temp directory
```
Error: Cannot create temp directory
Reason: {error_message}
Solution: Check disk space, verify temp directory permissions
```

**Error:** Cannot cleanup temp directory
```
Warning: Cannot cleanup temp directory {temp_dir}
Reason: {error_message}
Solution: Manual cleanup may be required
```

---

## Best Practices

### 1. Cache Directives in Memory
- Don't write directives to disk
- Store in memory for entire execution
- Reuse across phases

### 2. Verify Downloads
- Always verify script download succeeded
- Check file exists before execution
- Verify file size is reasonable

### 3. Always Cleanup
- Use try/finally for cleanup
- Remove temp directory even on errors
- Log cleanup failures as warnings

### 4. Handle Errors Gracefully
- Provide clear error messages
- Suggest solutions
- Fallback to alternative methods when possible

### 5. Prefer MCP Tools
- Use Firecrawl/Tavily/Browser MCP when available
- Fallback to curl/Python urllib if needed
- Document which method was used

### 6. Retry Logic
- Retry failed downloads (max 3 attempts)
- Exponential backoff for retries
- Log retry attempts

---

## Testing

### Test Cases

1. **Fetch Directives from Local:**
   - Verify all directives loaded
   - Verify content is correct
   - Verify no network calls

2. **Fetch Directives from GitHub:**
   - Verify all directives fetched
   - Verify content matches repository
   - Verify MCP tools work

3. **Download Scripts from GitHub:**
   - Verify all scripts downloaded
   - Verify scripts are executable
   - Verify temp directory created

4. **Execute Downloaded Scripts:**
   - Verify scripts execute correctly
   - Verify output is correct
   - Verify exit codes

5. **Cleanup:**
   - Verify temp directory removed
   - Verify cleanup on errors
   - Verify no leftover files

---

## Advanced: Authentication

### Private GitHub Repository

**Using Personal Access Token (PAT):**
```python
# Include token in URL
url = f"https://{token}@raw.githubusercontent.com/user/repo/branch/path"
```

**Security Note:** Don't commit tokens. Use environment variables or secure storage.

### Custom URL Authentication

**Using HTTP Basic Auth:**
```python
import base64

# Encode credentials
credentials = base64.b64encode(f"{username}:{password}".encode()).decode()
headers = {"Authorization": f"Basic {credentials}"}

# Use in request
# (Implementation depends on tool used)
```

---

## References

- [SOP Source Detector Guide](./sop-source-detector.md) - How to detect source
- [GitHub Setup Guide](./GITHUB_SETUP.md) - How to set up GitHub repository
- [Testing Guide](./TESTING_GUIDE.md) - How to test file fetching

---

**Version:** 1.0.0  
**Last Updated:** 2025-12-23  
**Status:** Production Ready  
**Next:** Use with source detector guide to complete implementation

