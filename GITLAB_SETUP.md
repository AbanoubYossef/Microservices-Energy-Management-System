# GitLab Setup Instructions

## Assignment Submission Requirements

**Repository Name Format**: `DS2025_Group_LastName_FirstName_Assignment_1`

For example: `DS2025_Group_Youssef_Abanoub_Assignment_1`

---

## Step 1: Create GitLab Repository

1. Go to: https://gitlab.com
2. Sign in with your account
3. Click **"New project"** button
4. Click **"Create blank project"**
5. Enter project name: `DS2025_Group_Youssef_Abanoub_Assignment_1`
6. Set visibility to **Private**
7. **Uncheck** "Initialize repository with a README"
8. Click **"Create project"**

---

## Step 2: Add GitLab as Remote

Open PowerShell in your project directory and run:

```powershell
# Add GitLab remote (replace with your actual GitLab URL)
git remote add gitlab https://gitlab.com/YOUR_USERNAME/DS2025_Group_Youssef_Abanoub_Assignment_1.git

# Verify remotes
git remote -v
```

You should see:
```
gitlab  https://gitlab.com/YOUR_USERNAME/DS2025_Group_Youssef_Abanoub_Assignment_1.git (fetch)
gitlab  https://gitlab.com/YOUR_USERNAME/DS2025_Group_Youssef_Abanoub_Assignment_1.git (push)
origin  https://github.com/AbanoubYossef/Microservices-Energy-Management-System.git (fetch)
origin  https://github.com/AbanoubYossef/Microservices-Energy-Management-System.git (push)
```

---

## Step 3: Push to GitLab

```powershell
# Push all branches to GitLab
git push gitlab main

# Or push with upstream tracking
git push -u gitlab main
```

If prompted for credentials:
- Username: Your GitLab username
- Password: Use a **Personal Access Token** (not your password)

### Creating Personal Access Token:
1. Go to GitLab → Settings → Access Tokens
2. Name: "DS2025 Assignment"
3. Scopes: Check **"write_repository"**
4. Click **"Create personal access token"**
5. Copy the token and use it as password

---

## Step 4: Share Repository with Instructor

1. Go to your GitLab project
2. Click **Settings** → **Members**
3. Click **"Invite members"**
4. Enter username: **`utcn_dsrl`**
5. Choose role: **Developer** or **Maintainer**
6. Click **"Invite"**

---

## Step 5: Verify Submission

Check that your repository contains:

### Required Files:
- ✅ Source code (all microservices)
- ✅ `docker-compose.yml`
- ✅ `README.md`
- ✅ Deployment diagram (PNG/PDF)
- ✅ `.puml` files (PlantUML source)

### Directory Structure:
```
DS2025_Group_Youssef_Abanoub_Assignment_1/
├── auth_service/
├── user_service/
├── device_service/
├── frontend/
├── traefik/
├── docker-compose.yml
├── README.md
├── deployment-diagram.png
├── deployment-diagram.puml
├── DEPLOYMENT_DIAGRAM.md
└── ... (other documentation files)
```

---

## Quick Commands Reference

```powershell
# Check current remotes
git remote -v

# Add GitLab remote
git remote add gitlab https://gitlab.com/YOUR_USERNAME/REPO_NAME.git

# Push to GitLab
git push gitlab main

# Push to both GitHub and GitLab
git push origin main
git push gitlab main

# Remove a remote (if needed)
git remote remove gitlab
```

---

## Alternative: Mirror from GitHub to GitLab

If you want to keep both repositories in sync:

```powershell
# Add GitLab as a push URL to origin
git remote set-url --add --push origin https://gitlab.com/YOUR_USERNAME/DS2025_Group_Youssef_Abanoub_Assignment_1.git

# Now git push will push to both
git push origin main
```

---

## Troubleshooting

### Issue: Authentication Failed
**Solution**: Use Personal Access Token instead of password

### Issue: Repository Already Exists
**Solution**: 
```powershell
git remote remove gitlab
git remote add gitlab NEW_URL
```

### Issue: Large Files
**Solution**: Make sure you're not pushing:
- `node_modules/` (should be in .gitignore)
- `.venv/` or `venv/` (should be in .gitignore)
- `__pycache__/` (should be in .gitignore)
- Large binary files

### Issue: Permission Denied
**Solution**: Make sure you've shared the repository with `utcn_dsrl`

---

## Your Current Setup

**GitHub Repository**: https://github.com/AbanoubYossef/Microservices-Energy-Management-System

**GitLab Repository**: (To be created)
- Name: `DS2025_Group_Youssef_Abanoub_Assignment_1`
- Visibility: Private
- Shared with: `utcn_dsrl`

**Gateway IP**: `172.18.0.3`

**Service IPs**:
- Frontend: `172.18.0.2`
- Traefik: `172.18.0.3`
- PostgreSQL: `172.18.0.4`
- Device Service: `172.18.0.5`
- Auth Service: `172.18.0.6`
- User Service: `172.18.0.7`

---

## Submission Checklist

Before final submission, verify:

- ✅ Repository name follows format: `DS2025_Group_LastName_FirstName_Assignment_1`
- ✅ All source code pushed (not archived)
- ✅ README.md with build and execution instructions
- ✅ UML Deployment Diagram included
- ✅ docker-compose.yml present
- ✅ Repository shared with `utcn_dsrl`
- ✅ No unnecessary files (node_modules, .venv, etc.)
- ✅ All services can be started with `docker-compose up`
- ✅ Swagger documentation accessible

---

## Final Steps

1. Create GitLab repository with correct name
2. Add GitLab as remote
3. Push all code to GitLab
4. Share repository with `utcn_dsrl`
5. Verify everything is accessible
6. Test that instructor can clone and run your project

---

**Good luck with your submission!** 🚀
