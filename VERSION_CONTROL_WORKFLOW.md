# AxonIntegrity Version Control Workflow

## Git Branching Strategy

### Branch Types

1. **`main`** - Production-ready code
   - Always deployable
   - Protected branch (no direct commits)
   - Requires pull request for changes

2. **`develop`** - Integration branch
   - Latest development changes
   - Pre-production testing
   - Merges to `main` for releases

3. **`feature/*`** - New features
   - Branch from `develop`
   - Naming: `feature/description-of-feature`
   - Example: `feature/stripe-payment-integration`

4. **`bugfix/*`** - Bug fixes
   - Branch from `develop` or `main`
   - Naming: `bugfix/description-of-bug`
   - Example: `bugfix/webhook-timeout-error`

5. **`hotfix/*`** - Emergency production fixes
   - Branch from `main`
   - Merge to both `main` and `develop`
   - Example: `hotfix/security-vulnerability`

---

## Feature Branch Workflow

### Step 1: Create Feature Branch

```bash
# Make sure you're on develop
git checkout develop
git pull origin develop

# Create new feature branch
git checkout -b feature/your-feature-name

# Example: Adding Stripe payment integration
git checkout -b feature/stripe-payment-integration
```

### Step 2: Work on Feature

```bash
# Make changes to your code
# Edit files, add new files, etc.

# Check what changed
git status

# Stage changes
git add .

# Or stage specific files
git add src/app.py src/services/stripe_client.py

# Commit with descriptive message
git commit -m "Add Stripe payment integration for B2C tier"

# Push to GitHub
git push origin feature/stripe-payment-integration
```

### Step 3: Keep Feature Branch Updated

```bash
# Regularly sync with develop to avoid conflicts
git checkout develop
git pull origin develop

git checkout feature/stripe-payment-integration
git merge develop

# Or use rebase for cleaner history
git rebase develop
```

### Step 4: Complete Feature

```bash
# Final commit
git add .
git commit -m "Complete Stripe integration with tests"
git push origin feature/stripe-payment-integration

# Merge back to develop
git checkout develop
git pull origin develop
git merge feature/stripe-payment-integration
git push origin develop

# Delete feature branch (optional)
git branch -d feature/stripe-payment-integration
git push origin --delete feature/stripe-payment-integration
```

---

## Commit Message Guidelines

### Format
```
<type>: <subject>

<body (optional)>

<footer (optional)>
```

### Types
- **feat:** New feature
- **fix:** Bug fix
- **docs:** Documentation changes
- **style:** Code formatting (no logic change)
- **refactor:** Code restructuring (no behavior change)
- **test:** Adding or updating tests
- **chore:** Maintenance tasks

### Examples

**Good:**
```
feat: Add Stripe payment integration for B2C tier

- Implement payment intent creation
- Add webhook handler for payment confirmation
- Create customer portal for subscription management

Closes #42
```

**Good:**
```
fix: Resolve SignalHire webhook timeout issue

The webhook handler was blocking on large batches.
Changed to async processing with background tasks.

Fixes #38
```

**Bad:**
```
updated stuff
```

**Bad:**
```
fixed bug
```

---

## Daily Workflow

### Morning Routine
```bash
# Start your day
cd C:\Users\gary_\Github-Repositories\axonintegrity-platform
git checkout develop
git pull origin develop

# Check what you're working on
git branch

# Create or switch to feature branch
git checkout feature/your-current-feature
```

### During Development
```bash
# Commit frequently (every logical change)
git add .
git commit -m "feat: Add email validation to contact form"

# Push to GitHub regularly (backup + collaboration)
git push origin feature/your-current-feature
```

### End of Day
```bash
# Final commit and push
git add .
git commit -m "WIP: Email validation - needs testing"
git push origin feature/your-current-feature

# Document progress in tasks/todo.md
```

---

## Working with Multiple Repos

### Your Current Repos
1. `axonintegrity-platform` - Main application
2. `aranya-platform-scorer` - Legacy HireJourne version
3. `axonintegrity-email-enrichment` - Unknown status

### Recommended Consolidation

**Option A: Single Repo (Recommended for solo developer)**
```bash
# Use axonintegrity-platform as the main repo
# Archive or delete other repos to avoid confusion
```

**Option B: Multiple Repos (If truly different products)**
```bash
# axonintegrity-platform - Main web application
# axonintegrity-tools - Standalone CLI tools
# axonintegrity-docs - Documentation site
```

---

## Emergency Procedures

### Undo Last Commit (Not Pushed)
```bash
git reset --soft HEAD~1  # Keep changes, undo commit
git reset --hard HEAD~1  # Discard changes, undo commit
```

### Undo Last Commit (Already Pushed)
```bash
git revert HEAD
git push origin feature/your-branch
```

### Discard All Local Changes
```bash
git checkout .
git clean -fd
```

### Recover Deleted Branch
```bash
git reflog
git checkout -b recovered-branch <commit-hash>
```

---

## Pre-Deployment Checklist

Before deploying to VPS:

- [ ] All tests pass locally
- [ ] Code committed to feature branch
- [ ] Feature branch merged to `develop`
- [ ] `.env.example` updated with new variables
- [ ] `requirements.txt` updated with new dependencies
- [ ] `README.md` updated with new features
- [ ] `REVISION_LOG.md` updated with changes
- [ ] No sensitive data in commits (API keys, passwords)
- [ ] Tested on Windows (your dev environment)

---

## Quick Reference

```bash
# Create feature branch
git checkout -b feature/name

# Stage and commit
git add .
git commit -m "feat: description"

# Push to GitHub
git push origin feature/name

# Merge to develop
git checkout develop
git merge feature/name
git push origin develop

# Deploy to production
git checkout main
git merge develop
git push origin main
# Then SSH to VPS and pull changes
```

---

## GitHub Integration

### Create Pull Request (Optional for solo dev)
1. Push feature branch to GitHub
2. Go to GitHub repo
3. Click "Compare & pull request"
4. Add description
5. Merge when ready

### Protect Main Branch
1. Go to repo Settings → Branches
2. Add rule for `main`
3. Require pull request reviews (optional)
4. Require status checks to pass

---

## Next Steps

1. **Initialize `.github` repo on GitHub**
2. **Set up `tasks/` directory in main repo**
3. **Create first feature branch**
4. **Test workflow with small change**
5. **Deploy to VPS from `main` branch**
