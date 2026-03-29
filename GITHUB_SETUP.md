# Push Code to GitHub Repository

## Prerequisites
1. **Git installed** - Download from https://git-scm.com/download/win
2. **GitHub account** - You have: `prabhakarmdes12-cmyk`
3. **Remote repository URL**: `https://github.com/prabhakarmdes12-cmyk/Bighi_Brothers_v2.git`

---

## Step-by-Step Instructions

### Step 1: Open Git Bash or Command Prompt
Open a terminal in your project folder:
```
c:/Users/User/Documents/Bighi Brothers/Bighi_Brothers_Website
```

### Step 2: Initialize Git Repository (if not already done)
```bash
git init
```

### Step 3: Configure Git (first time only)
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Step 4: Add All Files to Staging
```bash
git add .
```

### Step 5: Create Initial Commit
```bash
git commit -m "Initial commit - Bighi Brothers Website"
```

### Step 6: Add Remote Repository
```bash
git remote add origin https://github.com/prabhakarmdes12-cmyk/Bighi_Brothers_v2.git
```

### Step 7: Push to GitHub
```bash
git branch -M main
git push -u origin main
```

---

## Troubleshooting

### If you get authentication errors:
1. Generate a Personal Access Token from GitHub:
   - Go to GitHub Settings → Developer settings → Personal access tokens
   - Generate new token with `repo` scope
2. Use the token as your password when prompted

### If remote already exists:
```bash
git remote set-url origin https://github.com/prabhakarmdes12-cmyk/Bighi_Brothers_v2.git
```

### Verify remote is set correctly:
```bash
git remote -v
```

---

## Files in This Repository
- HTML files (main pages, shop, admin, journal)
- Documentation (TECHNICAL_DOCUMENTATION, AUDIT_REPORT, etc.)
- Assets (logo)
