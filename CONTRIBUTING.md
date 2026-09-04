# Contributing Guidelines

**Thank you for your interest in contributing!**

Before contributing to this repository, please read and understand these guidelines carefully.

## 1. Access & Authorization
- 🔐 **Private Repository**: This is a private repository
- ✅ **Contributors Only**: Only authorized collaborators may contribute
- 📝 **NDA Required**: Contributors must sign a Non-Disclosure Agreement
- ✉️ **Request Access**: Email kajwang230@gmail.com to request contributor status

**Unauthorized contributions will be rejected and may result in legal action.**

## 2. Code of Conduct
- ✅ Respect intellectual property rights
- ✅ Keep code and discussions confidential
- ✅ Follow coding standards and best practices
- ✅ Communicate professionally and respectfully
- ❌ Do not copy code from other sources without attribution
- ❌ Do not share code with unauthorized parties

## 3. Before You Start
1. **Read the LICENSE.md** - Understand ownership and usage restrictions
2. **Read the SECURITY.md** - Understand security requirements
3. **Sign the NDA** - Required for all contributors (if applicable)
4. **Get explicit permission** - Confirm your role and scope with the Owner

## 4. Contribution Workflow

### Step 1: Create a Feature Branch
```bash
git checkout -b feature/your-feature-name
# or
git checkout -b bugfix/bug-description
```

**Branch naming conventions:**
- `feature/` - New features
- `bugfix/` - Bug fixes
- `refactor/` - Code refactoring
- `docs/` - Documentation updates
- `security/` - Security improvements

### Step 2: Make Your Changes
- Write clean, readable code
- Add comments for complex logic
- Follow existing code style
- Keep commits atomic and logical

### Step 3: Test Your Changes
```bash
# Run tests before pushing
npm test          # or
python -m pytest  # or
./gradlew test    # etc.
```

### Step 4: Commit with Clear Messages
```bash
git commit -m "feat: add new authentication module"
git commit -m "fix: resolve memory leak in database connection"
git commit -m "docs: update API documentation"
```

**Commit message format:**
- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation
- `refactor:` Code refactoring
- `test:` Tests
- `security:` Security improvements

### Step 5: Push & Create Pull Request
```bash
git push origin feature/your-feature-name
```

Then create a Pull Request with:
- Clear title describing changes
- Detailed description of what and why
- Reference to any related issues
- Screenshots/demos if applicable

## 5. Pull Request Requirements
Your PR must include:
- ✅ Clear, descriptive title
- ✅ Detailed description of changes
- ✅ Tests (if applicable)
- ✅ No breaking changes (unless approved)
- ✅ Updated documentation
- ✅ No merge conflicts
- ✅ Code review approval

**PRs that don't meet these requirements will be rejected.**

## 6. Security Requirements
- ❌ **Never commit secrets** (API keys, passwords, tokens)
- ❌ **Never commit credentials** in `.env` files
- ✅ Use `.gitignore` to exclude sensitive files:
  ```
  .env
  .env.local
  .env.*.local
  node_modules/
  build/
  dist/
  .DS_Store
  *.log
  ```
- ✅ Use GitHub Secrets for sensitive configuration
- ✅ Scan for vulnerabilities before pushing
- ✅ Sign commits with GPG (recommended):
  ```bash
  git config --global user.signingkey <your-key-id>
  git commit -S -m "your message"
  ```

## 7. Code Quality Standards
- 📝 **Code Style**: Follow existing patterns and conventions
- 🧪 **Testing**: Write tests for new features (minimum 80% coverage)
- 📖 **Documentation**: Document public APIs and complex logic
- 🔍 **Code Review**: All code must pass review before merge
- ⚙️ **Dependencies**: Get approval before adding new dependencies

## 8. Documentation
Update documentation for:
- New features
- API changes
- Configuration changes
- Security updates

Use clear language and include examples.

## 9. Prohibited Actions
You may **NOT**:
- ❌ Copy code to public repositories
- ❌ Share code with unauthorized parties
- ❌ Use code for unauthorized commercial purposes
- ❌ Violate the LICENSE.md terms
- ❌ Commit security vulnerabilities
- ❌ Remove copyright notices
- ❌ Disable or bypass security measures

**Violations will result in access revocation and possible legal action.**

## 10. Review Process
1. **Automated Checks**: GitHub Actions runs tests and linters
2. **Code Review**: Owner reviews code for quality, security, compliance
3. **Feedback**: Changes may be requested
4. **Approval**: PR must be approved before merging
5. **Merge**: Only Owner merges approved PRs

**Expected review time: 2-5 business days**

## 11. Issue Reporting
Found a bug or have a feature request?

1. Check if it's already reported
2. Create an issue with:
   - Clear title
   - Detailed description
   - Steps to reproduce (bugs)
   - Expected vs actual behavior
   - Environment details

**Note**: Only authorized contributors can create issues.

## 12. Security Issues
**CRITICAL**: Never create a public issue for security vulnerabilities.

Instead:
1. Email kajwang230@gmail.com
2. Include: description, impact, reproduction steps
3. Do not disclose publicly
4. Allow 30 days for response

## 13. Commit Signing
It's recommended to sign commits for authenticity:

```bash
# Generate GPG key
gpg --full-generate-key

# Configure Git
git config --global user.signingkey <your-key-id>

# Sign commits
git commit -S -m "commit message"

# Verify signature
git log --show-signature
```

## 14. Merge Policy
- ✅ Only Owner can merge PRs
- ✅ Squash commits for cleaner history
- ✅ Delete branch after merge
- ✅ All checks must pass
- ✅ All reviews must approve

## 15. Post-Merge
After your code is merged:
- ✅ Delete your feature branch
- ✅ Update any linked documentation
- ✅ Notify relevant stakeholders
- ✅ Monitor for issues

## 16. Questions & Support
- 📧 Email: kajwang230@gmail.com
- 🔗 LinkedIn: https://www.linkedin.com/in/patience-kajwang-b239a5253
- 💬 Slack/Teams: (if available)

## 17. Acknowledgment
By contributing to this repository, you agree to:
1. Follow all guidelines in this document
2. Respect the LICENSE.md terms
3. Keep code confidential
4. Comply with security requirements
5. Accept that violations may result in legal action

---

**Last Updated**: September 2026

**Questions? Contact kajwang230@gmail.com**

Thank you for your contributions! 🎉
