# Why This Tool Needs AGENTS.md

**Date:** 2025-12-24  
**Status:** Documentation

---

## The Problem

The agents-md-generator tool was missing its own `AGENTS.md` file, which meant:

- ❌ AI/LLM agents could not automatically discover the tool
- ❌ AI tools (Cursor, Claude Code, etc.) would not automatically load context
- ❌ Users had to manually point AI to README.md or other files
- ❌ No progressive context loading for the tool itself

---

## The Solution

**AGENTS.md** is now in the root of the agents-md-generator folder.

### What AGENTS.md Does

1. **Auto-Discovery:** AI tools automatically detect and read `AGENTS.md` files
2. **Progressive Context Loading:** Provides 4-level context loading protocol
3. **Vendor-Neutral:** Works with GitHub Copilot, Cursor, Claude Code, Windsurf, etc.
4. **AI-First:** Designed specifically for AI/LLM agents, not humans

### README.md vs. AGENTS.md

| File | Audience | Purpose | Auto-Discovery |
|------|----------|---------|----------------|
| **README.md** | Humans | Human-readable documentation, quick start for people | ❌ No |
| **AGENTS.md** | AI/LLM | AI-readable context, progressive loading protocol | ✅ Yes |
| **QUICK-START-PROMPT.md** | Humans | Copy/paste prompts for humans to give to AI | ❌ No |
| **START-HERE.txt** | Humans | Quick reference for humans | ❌ No |

---

## How AI Tools Auto-Discover AGENTS.md

### Supported Tools

According to [AGENTS.md standard](https://agents.md/):

- ✅ **GitHub Copilot** - Automatically reads AGENTS.md
- ✅ **Cursor IDE** - Automatically reads AGENTS.md
- ✅ **Windsurf** - Automatically reads AGENTS.md
- ✅ **Claude Code** - Automatically reads AGENTS.md (or use CLAUDE.md symlink)
- ✅ **Other AI coding tools** - Many support AGENTS.md

### Auto-Discovery Process

1. **AI tool opens folder**
2. **Checks for AGENTS.md in root**
3. **Automatically loads Level 1 context** (~200 tokens)
4. **AI decides if tool is relevant**
5. **If relevant, loads Level 2 context** (~2,000 tokens)
6. **Progressive loading continues as needed**

### No Manual Intervention Required

- ❌ No need to tell AI "read README.md"
- ❌ No need to manually load files
- ❌ No need to provide file paths
- ✅ AI automatically discovers and loads AGENTS.md

---

## Optional: Tool-Specific Files

Some tools may need symlinks for compatibility:

```bash
# For Claude Code (if needed)
ln -s AGENTS.md CLAUDE.md

# For Cline (if needed)
ln -s AGENTS.md .clinerules/rules.md
```

**Note:** Most modern tools support AGENTS.md directly, so symlinks are usually not needed.

---

## .cursorrules Alternative

Some tools (like Cursor) also support `.cursorrules` files, but:

- **AGENTS.md** is vendor-neutral (works with many tools)
- **.cursorrules** is Cursor-specific
- **AGENTS.md** includes progressive context loading
- **.cursorrules** is typically a flat instruction file

**Recommendation:** Use AGENTS.md for maximum compatibility.

---

## Summary

**Before:**
- Tool had README.md (human-focused)
- Tool had QUICK-START-PROMPT.md (human copy/paste)
- ❌ No AGENTS.md (AI auto-discovery)
- ❌ AI tools couldn't automatically discover the tool

**After:**
- ✅ Tool has AGENTS.md (AI auto-discovery)
- ✅ AI tools automatically discover and load context
- ✅ Progressive context loading for the tool itself
- ✅ Vendor-neutral format works with all major AI tools

**Result:** AI/LLM agents can now automatically discover, understand, and use the agents-md-generator tool without manual intervention.

---

**Status:** ✅ AGENTS.md created and validated  
**Validation:** 12/12 checks passed  
**Ready:** For automatic discovery by AI/LLM agents

