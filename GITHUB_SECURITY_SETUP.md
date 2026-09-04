# GitHub Security Setup Guide

## Complete Security Configuration for Your Repositories

This guide provides step-by-step instructions to secure your GitHub account and repositories against unauthorized access and code theft.

---

## 1. GitHub Account Security

### 1.1 Enable Two-Factor Authentication (2FA)
**CRITICAL: Required for all contributors**

**Steps:**
1. Go to GitHub Settings → Security
2. Click "Enable two-factor authentication"
3. Choose authentication method:
   - ✅ **Authenticator App** (Recommended): Google Authenticator, Microsoft Authenticator, Authy
   - ✅ **SMS**: Text message codes
4. Save recovery codes in a **secure location** (password manager, safe)
5. Confirm setup

```
GitHub Settings → Account Security → Two-Factor Authentication → Enable
```

**Why 2FA is Critical:**
- 🔒 Prevents account takeover even if password is compromised
- 🛡️ Protects your code from theft
- 📱 Recovery codes ensure access if you lose your device

### 1.2 Create & Manage Personal Access Tokens (PAT)

**For CLI and API access (instead of password):**

1. Go to Settings → Developer settings → Personal access tokens
2. Click "Generate new token"
3. Set scopes:
   - ✅ `repo` (full control of repositories)
   - ✅ `read:user` (read user profile)
   - ✅ `gist` (create gists)
4. Set expiration: **90 days maximum**
5. Copy token immediately (won't be shown again)
6. Store in secure password manager (NOT in code)

**Security Tips:**
- ❌ Never commit PAT to repository
- ❌ Never share PAT with others
- ✅ Rotate tokens every 90 days
- ✅ Delete unused tokens
- ✅ Use minimal scopes needed

### 1.3 Manage SSH Keys

**For secure Git operations:**

**Generate SSH Key (if not already done):**
```bash
ssh-keygen -t ed25519 -C "kajwang230@gmail.com"
# or for older systems:
ssh-keygen -t rsa -b 4096 -C "kajwang230@gmail.com"
```

**Add to GitHub:**
1. Go to Settings → SSH and GPG keys
2. Click "New SSH key"
3. Paste public key (`~/.ssh/id_ed25519.pub`)
4. Give it a descriptive title: "Work Laptop 2024"
5. Click "Add SSH key"

**Use SSH for Git operations:**
```bash
# Clone with SSH
git clone git@github.com:Kajwang230/repo-name.git

# Push/Pull use SSH automatically
git push origin main
```

**Security:**
- ✅ SSH is more secure than HTTPS
- ✅ No need to enter credentials repeatedly
- ❌ Never share private key
- ✅ Use passphrase on private key

### 1.4 GPG Signing for Commits

**Sign commits to prove authenticity:**

**Generate GPG Key:**
```bash
gpg --full-generate-key
# Follow prompts:
# - Kind: RSA and RSA (default)
# - Length: 4096
# - Real name: Patience Kajwang Omondi
# - Email: kajwang230@gmail.com
```

**Get your key ID:**
```bash
gpg --list-secret-keys --keyid-format=long
# Copy the key ID (16 characters after "sec")
```

**Add to GitHub:**
1. Go to Settings → SSH and GPG keys
2. Click "New GPG key"
3. Export and paste your public key:
   ```bash
   gpg --armor --export YOUR_KEY_ID
   ```
4. Click "Add GPG key"

**Configure Git:**
```bash
git config --global user.signingkey YOUR_KEY_ID
git config --global commit.gpgsign true
```

**Sign commits:**
```bash
# Automatic (if configured globally)
git commit -m "your message"

# Manual
git commit -S -m "your message"

# Verify signatures
git log --show-signature
```

**Benefits:**
- ✅ Proves you made the commit
- ✅ Prevents impersonation
- ✅ Shows "Verified" badge on GitHub

---

## 2. Repository Security

### 2.1 Repository Visibility & Access Control

**Ensure Repository is Private:**
1. Go to Repository Settings → General
2. Under "Danger Zone" → Repository visibility
3. Confirm it's set to **PRIVATE** ✅
4. Click "Make private" if needed

**Manage Access:**
1. Go to Settings → Collaborators and teams
2. Only add **authorized users**
3. Set appropriate roles:
   - 👤 **Maintain**: Can push, review PRs, manage settings
   - 📝 **Write**: Can push and review PRs
   - 👁️ **Read**: View only (for auditing)
4. Remove inactive/unauthorized users immediately

**Add Collaborators:**
1. Go to Settings → Collaborators and teams
2. Click "Add people"
3. Enter GitHub username
4. Set role and click "Add"
5. They'll receive an invitation

### 2.2 Branch Protection Rules

**Protect main/master branch:**

1. Go to Settings → Branches
2. Click "Add rule" under Branch protection rules
3. Set branch name pattern: `main` or `master`
4. Enable protections:
   - ✅ **Require pull request reviews**: 1-2 reviews minimum
   - ✅ **Require status checks to pass**: All CI/CD checks
   - ✅ **Dismiss stale PR approvals**: Re-review after new commits
   - ✅ **Require branches to be up to date**: Before merging
   - ✅ **Require code review from code owners**: If using CODEOWNERS
   - ✅ **Require approval of the latest reviewable push**: Latest version only
   - ✅ **Restrict who can push to matching branches**: Only admins

**Benefits:**
- 🛡️ Prevents accidental merges
- 🔍 Forces code review
- ✅ Ensures quality standards

### 2.3 Enable Branch Auto-Delete

**Clean up branches automatically:**
1. Settings → General
2. Enable "Automatically delete head branches"
3. This removes feature branches after PR merge

### 2.4 Require Signed Commits

**Enforce GPG-signed commits:**

1. Settings → Branches
2. Edit main branch protection rule
3. Enable: **Require signed commits**
4. Now all commits must be signed

---

## 3. Secrets Management

### 3.1 GitHub Secrets for Sensitive Data

**Never commit secrets. Use GitHub Secrets instead.**

**Add a Secret:**
1. Go to Settings → Secrets and variables → Actions
2. Click "New repository secret"
3. Name: `DATABASE_URL`, `API_KEY`, etc.
4. Value: Your actual secret
5. Click "Add secret"

**Use in GitHub Actions:**
```yaml
- name: Deploy
  env:
    DATABASE_URL: ${{ secrets.DATABASE_URL }}
    API_KEY: ${{ secrets.API_KEY }}
  run: npm run deploy
```

**Best Practices:**
- ❌ Never log secrets to console
- ✅ Use `***` masking in logs
- ✅ Rotate secrets regularly
- ✅ Use least-privilege access
- ✅ Audit secret usage

### 3.2 Protect Sensitive Environment Variables

**In `.env` files (add to `.gitignore`):**
```bash
# .env (NEVER COMMIT)
DATABASE_URL=postgresql://user:password@localhost/db
API_KEY=sk_test_xxxxxxxxxxxxx
JWT_SECRET=your_secret_key
```

**Use `.env.example` instead:**
```bash
# .env.example (COMMIT THIS)
DATABASE_URL=<your_database_url>
API_KEY=<your_api_key>
JWT_SECRET=<your_jwt_secret>
```

---

## 4. Monitoring & Auditing

### 4.1 Enable Audit Logs

**Track all repository activity:**

1. Settings → Audit log
2. View all actions: pushes, PRs, user management, etc.
3. Monitor for suspicious activity
4. Review regularly (weekly recommended)

**Check for:**
- 🔍 Unauthorized access attempts
- 📝 Unexpected changes
- 👥 Unrecognized users
- 🗑️ Deleted files or branches

### 4.2 Enable Notifications

**Stay informed of repository activity:**

1. Go to Notification settings (bell icon → settings)
2. Enable notifications for:
   - ✅ Pull request reviews
   - ✅ Security alerts
   - ✅ Repository changes
   - ✅ Mentions
3. Set frequency: Real-time or digest

### 4.3 Security Alerts

**Enable Dependabot alerts:**
1. Settings → Code security and analysis
2. Enable:
   - ✅ Dependabot alerts
   - ✅ Dependabot security updates
   - ✅ Secret scanning
   - ✅ Push protection

**This will:**
- 🚨 Alert on vulnerable dependencies
- 🔍 Detect leaked secrets
- 🛡️ Block pushes with exposed secrets

---

## 5. Advanced Security Features

### 5.1 CODEOWNERS File

**Require specific users to review changes:**

Create `.github/CODEOWNERS`:
```
# Security files - require Owner review
SECURITY.md @Kajwang230
LICENSE.md @Kajwang230
.github/workflows/ @Kajwang230

# Database files - require database expert
src/database/ @database-expert

# Frontend - require frontend lead
src/frontend/ @frontend-lead
```

**Benefits:**
- 👥 Ensures appropriate expertise reviews code
- 🛡️ Prevents unauthorized changes to sensitive files
- 🔐 Adds extra layer of protection

### 5.2 Required Status Checks

**Ensure all tests pass before merge:**

1. Settings → Branches → Branch protection
2. Under "Status checks that are required to pass before merging"
3. Select required checks:
   - ✅ Tests pass
   - ✅ Linting passes
   - ✅ Security scan passes
   - ✅ Build succeeds

### 5.3 Restrict Force Pushes

**Prevent accidental history rewriting:**

1. Settings → Branches → Branch protection
2. Enable: **Restrict who can force push**
3. Only admins can force push

---

## 6. Security Checklist

### Account Security
- [ ] Two-Factor Authentication (2FA) enabled
- [ ] Strong, unique password (20+ characters)
- [ ] SSH keys configured
- [ ] GPG signing configured
- [ ] Recovery codes saved securely
- [ ] No PAT stored in code or files
- [ ] Regular password rotation (every 90 days)

### Repository Security
- [ ] Repository set to PRIVATE
- [ ] Only authorized collaborators added
- [ ] Branch protection enabled on main
- [ ] GPG signing required
- [ ] Code review required (1-2 reviewers)
- [ ] Status checks required
- [ ] CODEOWNERS file created
- [ ] Audit logs reviewed weekly
- [ ] Dependabot alerts enabled
- [ ] Secret scanning enabled

### Code Security
- [ ] `.gitignore` includes sensitive files
- [ ] No secrets in code/commits
- [ ] All dependencies up to date
- [ ] Security vulnerabilities fixed
- [ ] Commits signed with GPG
- [ ] Code reviews completed
- [ ] Tests pass before merge

### Access Control
- [ ] SSH configured (not HTTPS)
- [ ] PAT rotated (90 days max)
- [ ] Unused tokens deleted
- [ ] Inactive collaborators removed
- [ ] 2FA enforced for all
- [ ] Minimum required permissions

---

## 7. Responding to Security Incidents

### If You Suspect a Breach:

1. **Change Your Password Immediately**
   - Go to Settings → Password
   - Use strong, unique password
   - 20+ characters, mix of types

2. **Rotate All Secrets**
   - Regenerate API keys
   - Create new database passwords
   - Update environment variables

3. **Review Audit Log**
   - Check for unauthorized access
   - Look for suspicious commits/changes
   - Note timestamps and users

4. **Revoke Compromised Tokens**
   - Go to Settings → Developer settings
   - Delete suspicious PAT
   - Delete SSH keys if compromised

5. **Notify Collaborators**
   - Email: kajwang230@gmail.com
   - Explain the incident
   - Ask to rotate their credentials

6. **Force Password Reset for Contributors**
   - Settings → Collaborators
   - Remove and re-add users (forces reset)

---

## 8. Security Best Practices

### Daily Habits
- ✅ Lock your computer when away
- ✅ Never enter credentials on public Wi-Fi
- ✅ Use VPN for remote work
- ✅ Log out of GitHub when done
- ✅ Review recent activity regularly

### Development
- ✅ Never hardcode secrets
- ✅ Use `.env` for local config
- ✅ Use GitHub Secrets for CI/CD
- ✅ Sign all commits
- ✅ Use HTTPS or SSH (not HTTP)
- ✅ Keep dependencies updated

### Collaboration
- ✅ Only invite authorized users
- ✅ Verify new collaborators
- ✅ Remove inactive users
- ✅ Review PRs carefully
- ✅ Require approvals
- ✅ Monitor audit logs

### Incident Response
- ✅ Report security issues immediately
- ✅ Don't discuss publicly
- ✅ Rotate credentials regularly
- ✅ Keep recovery codes safe
- ✅ Have backup authentication methods

---

## 9. Useful Commands

```bash
# Clone with SSH
git clone git@github.com:Kajwang230/repo-name.git

# Set up GPG signing globally
git config --global user.signingkey YOUR_KEY_ID
git config --global commit.gpgsign true

# Sign a commit
git commit -S -m "your message"

# Verify commit signatures
git log --show-signature

# View GPG keys
gpg --list-secret-keys --keyid-format=long

# Export public GPG key
gpg --armor --export YOUR_KEY_ID

# Generate strong password (Linux/Mac)
openssl rand -base64 32

# Check SSH connection
ssh -T git@github.com
```

---

## 10. Emergency Contacts

**Security Issues:**
- 📧 Email: kajwang230@gmail.com
- 🔗 LinkedIn: https://www.linkedin.com/in/patience-kajwang-b239a5253

**GitHub Support:**
- 🌐 https://github.com/support
- 📧 support@github.com

---

## Compliance Checklist

- [ ] All requirements from SECURITY.md met
- [ ] All requirements from LICENSE.md understood
- [ ] All requirements from CONTRIBUTING.md followed
- [ ] All requirements from CODE_OF_CONDUCT.md accepted
- [ ] All requirements from this guide implemented
- [ ] Audit logs reviewed weekly
- [ ] No security incidents in last 30 days
- [ ] All team members trained on security

---

**Last Updated**: September 2026  
**Version**: 1.0  
**Status**: Active

*This guide should be reviewed and updated quarterly or after any security incident.*
