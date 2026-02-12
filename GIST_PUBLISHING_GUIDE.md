# GitHub Gist Publishing Guide
## JP Agent Flow - Multi-Agent Development System

This guide explains how to publish all 7 agent files as a single GitHub Gist and update the main documentation to reference it.

---

## 📋 Prerequisites

- GitHub account
- GitHub CLI (`gh`) installed and authenticated
- All 7 agent files in the `Agents/` folder

---

## 📦 Files to Include

Your Gist will contain these 7 agent definition files:

1. **orchestrator.agent.md** - Coordinates the full development lifecycle
2. **researcher.agent.md** - Investigates technologies and maps codebases
3. **planner.agent.md** - Creates roadmaps and implementation plans
4. **coder.agent.md** - Writes code following mandatory principles
5. **designer.agent.md** - Handles UI/UX design tasks
6. **verifier.agent.md** - Goal-backward verification of phase outcomes
7. **debugger.agent.md** - Scientific debugging with hypothesis testing

---

## 🚀 Step 1: Create the Multi-File Gist

### Using GitHub CLI (Recommended)

Open your terminal in the project root directory and run:

```powershell
gh gist create `
  "Agents/orchestrator.agent.md" `
  "Agents/researcher.agent.md" `
  "Agents/planner.agent.md" `
  "Agents/coder.agent.md" `
  "Agents/designer.agent.md" `
  "Agents/verifier.agent.md" `
  "Agents/debugger.agent.md" `
  --public `
  --desc "JP Agent Flow - Multi-Agent Development System"
```

**Expected Output:**
```
- Creating gist orchestrator.agent.md, researcher.agent.md, planner.agent.md, coder.agent.md, designer.agent.md, verifier.agent.md, debugger.agent.md
✓ Created gist orchestrator.agent.md
https://gist.github.com/YOUR_USERNAME/a1b2c3d4e5f6g7h8i9j0
```

### Using GitHub Web UI (Alternative)

If you prefer the web interface:

1. **Navigate to:** https://gist.github.com/
2. **Click:** "New gist" button (top right)
3. **Add files one by one:**
   - For each file, click "Add file" button
   - Copy filename from "Agents/" folder
   - Paste the content of each .md file
4. **Add description:** "JP Agent Flow - Multi-Agent Development System"
5. **Select:** "Create public gist"
6. **Click:** "Create secret gist" or "Create public gist" button

---

## 🔍 Step 2: Extract the Gist ID

### From GitHub CLI Output

The Gist ID is the alphanumeric string at the end of the URL:

```
https://gist.github.com/YOUR_USERNAME/a1b2c3d4e5f6g7h8i9j0
                                      └─────────────┬──────────┘
                                                 GIST_ID
```

**Example:**
- URL: `https://gist.github.com/jpetersen/a1b2c3d4e5f6g7h8i9j0`
- Gist ID: `a1b2c3d4e5f6g7h8i9j0`

### From Web UI

After creating the Gist, look at the browser address bar:

```
https://gist.github.com/YOUR_USERNAME/abc123def456
                                      └────┬──────┘
                                        GIST_ID
```

**💡 Tip:** The Gist ID is typically 32 characters long and contains lowercase letters and numbers.

---

## ✏️ Step 3: Update AGENTS_GIST.md

The `AGENTS_GIST.md` file contains placeholder `GIST_ID` references that need to be replaced with your actual Gist ID.

### Using PowerShell Find-Replace

```powershell
# Replace GIST_ID with your actual ID
(Get-Content "AGENTS_GIST.md") -replace 'GIST_ID', 'a1b2c3d4e5f6g7h8i9j0' | Set-Content "AGENTS_GIST.md"
```

**Replace:** `a1b2c3d4e5f6g7h8i9j0` with your actual Gist ID

### Using VS Code Find-Replace

1. **Open:** `AGENTS_GIST.md` in VS Code
2. **Press:** `Ctrl+H` (Windows/Linux) or `Cmd+H` (Mac)
3. **Find:** `GIST_ID`
4. **Replace:** Your actual Gist ID (e.g., `a1b2c3d4e5f6g7h8i9j0`)
5. **Click:** "Replace All" button
6. **Save:** `Ctrl+S` or `Cmd+S`

### Manual Find-Replace (Any Text Editor)

Search for all occurrences of `GIST_ID` and replace them with your actual Gist ID.

**Locations to update (typically):**
- Agent download links: `https://gist.githubusercontent.com/.../GIST_ID/raw/...`
- Gist view links: `https://gist.github.com/.../GIST_ID`

---

## ✅ Step 4: Verify the Links

After updating, verify that the links work:

### Test Raw File Links

Each agent file should be accessible via raw GitHub URLs:

```
https://gist.githubusercontent.com/YOUR_USERNAME/YOUR_GIST_ID/raw/orchestrator.agent.md
https://gist.githubusercontent.com/YOUR_USERNAME/YOUR_GIST_ID/raw/researcher.agent.md
https://gist.githubusercontent.com/YOUR_USERNAME/YOUR_GIST_ID/raw/planner.agent.md
https://gist.githubusercontent.com/YOUR_USERNAME/YOUR_GIST_ID/raw/coder.agent.md
https://gist.githubusercontent.com/YOUR_USERNAME/YOUR_GIST_ID/raw/designer.agent.md
https://gist.githubusercontent.com/YOUR_USERNAME/YOUR_GIST_ID/raw/verifier.agent.md
https://gist.githubusercontent.com/YOUR_USERNAME/YOUR_GIST_ID/raw/debugger.agent.md
```

**Test:** Open each URL in your browser - you should see the raw markdown content.

### Test Gist View Link

```
https://gist.github.com/YOUR_USERNAME/YOUR_GIST_ID
```

**Expected:** You should see all 7 files listed with tabs for each agent.

---

## 🔄 Step 5: Commit and Share

Once verified, commit your updated `AGENTS_GIST.md`:

```powershell
git add AGENTS_GIST.md
git commit -m "docs: update Gist ID with published agent files"
git push
```

---

## 🛠️ Troubleshooting

### Problem: "gh: command not found"

**Solution:** Install GitHub CLI
- **Windows:** `winget install GitHub.cli`
- **Mac:** `brew install gh`
- **Linux:** See https://github.com/cli/cli#installation

### Problem: "gh: authentication required"

**Solution:** Authenticate with GitHub
```powershell
gh auth login
```

Follow the prompts to authenticate via browser or token.

### Problem: Links return 404

**Possible causes:**
1. **Wrong Gist ID** - Double-check you copied the correct ID
2. **Private Gist** - Ensure the Gist is public
3. **Filename mismatch** - Verify filenames match exactly (case-sensitive)

**Solution:** 
- Verify Gist is public at `https://gist.github.com/YOUR_USERNAME/YOUR_GIST_ID`
- Check that filenames in the Gist match the URL paths exactly

### Problem: Can't find GIST_ID placeholders

**Possible causes:**
1. Already replaced in a previous run
2. Different placeholder format used

**Solution:**
- Search for your GitHub username in the file
- Look for gist.github.com or gist.githubusercontent.com URLs
- Manually verify URLs point to the correct Gist

### Problem: "Failed to create gist"

**Possible causes:**
1. File paths incorrect
2. Not in correct directory
3. Files don't exist

**Solution:**
```powershell
# Verify you're in the project root
Get-Location

# Verify files exist
Get-ChildItem Agents\*.agent.md

# Try with absolute paths
gh gist create (Get-ChildItem Agents\*.agent.md | ForEach-Object { $_.FullName })
```

---

## 📖 Understanding the URLs

### Raw Content URL Pattern
```
https://gist.githubusercontent.com/USERNAME/GIST_ID/raw/FILENAME
```

**Used for:** Direct file downloads, agent imports, automation

### Gist View URL Pattern
```
https://gist.github.com/USERNAME/GIST_ID
```

**Used for:** Human-readable view, sharing, editing

### Revision-Specific URL Pattern
```
https://gist.githubusercontent.com/USERNAME/GIST_ID/RAW_HASH/FILENAME
```

**Used for:** Pinning to specific version (auto-generated by GitHub)

**⚠️ Note:** The `/raw/` URL without a hash always points to the latest version.

---

## 🔐 Privacy Considerations

### Public Gists
- ✅ Accessible to everyone
- ✅ Indexed by search engines
- ✅ Can be forked and starred
- ✅ Ideal for sharing agent configurations

### Private/Secret Gists
- ✅ Only accessible via direct URL
- ❌ Not indexed, but not truly private
- ❌ Anyone with the URL can view
- ⚠️ Use for semi-private sharing only

**Recommendation:** Use public Gists for agent definitions unless they contain sensitive project-specific information.

---

## 📚 Next Steps

After publishing your Gist:

1. **Share the Gist URL** with your team or community
2. **Update documentation** in other projects that reference these agents
3. **Version control** - Consider creating new Gists for major version changes
4. **Fork & customize** - Users can fork your Gist to create their own variants

---

## 🎯 Quick Reference

**Create Gist:**
```powershell
gh gist create Agents/*.agent.md --public --desc "JP Agent Flow"
```

**Update placeholders:**
```powershell
(Get-Content "AGENTS_GIST.md") -replace 'GIST_ID', 'YOUR_GIST_ID' | Set-Content "AGENTS_GIST.md"
```

**Verify links:**
```powershell
# Open Gist in browser
gh gist view YOUR_GIST_ID --web
```

---

## 📞 Support

If you encounter issues:

1. **Check the Gist exists:** Visit `https://gist.github.com/YOUR_USERNAME/YOUR_GIST_ID`
2. **Verify authentication:** Run `gh auth status`
3. **Check file permissions:** Ensure all .agent.md files are readable
4. **Review GitHub status:** https://www.githubstatus.com/

---

**Last Updated:** February 12, 2026
**Document Version:** 1.0
**Compatibility:** GitHub CLI v2.0+, PowerShell 5.1+, VS Code 1.60+
