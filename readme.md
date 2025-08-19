## Create Custom Chat mode in copilot

### Prerequisites
- VS Code with GitHub Copilot extension installed
- Git configured on your machine
- GitHub account with Copilot access

### Step 1: Clone Repository and Verify Structure
```bash
# Clone the repository
git clone https://github.com/arpit20250701/Config-Modes.git
cd Config-Modes

# Verify required directories exist
ls -la .github/ .vscode/
```

**Required structure:**
```
.github/
├── copilot-instructions.md
└── prompts/
    └── 10-create-vision-doc.md
.vscode/
└── settings.json
```

**Troubleshooting:**
- If custom modes don't appear, check file permissions
- Ensure VS Code has latest Copilot extension
- Restart VS Code after adding files
