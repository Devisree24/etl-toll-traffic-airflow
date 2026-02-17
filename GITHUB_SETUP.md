# Steps to Push Project to GitHub

## Step 1: Create a GitHub Repository

1. Go to [GitHub.com](https://github.com) and sign in
2. Click the **"+"** icon in the top right corner
3. Select **"New repository"**
4. Fill in the details:
   - **Repository name**: `etl-toll-traffic-airflow` (or any name you prefer)
   - **Description**: "ETL pipeline for road traffic toll data using Apache Airflow"
   - **Visibility**: Choose Public or Private
   - **DO NOT** check "Initialize with README" (you already have one)
   - **DO NOT** add .gitignore or license (you already have them)
5. Click **"Create repository"**

## Step 2: Initialize Git in Your Local Project

Open PowerShell or Command Prompt and navigate to your project folder:

```powershell
cd c:\Users\devis\Downloads\etl-toll-traffic-airflow
```

Initialize Git repository:

```powershell
git init
```

## Step 3: Add All Files to Git

```powershell
git add .
```

This adds all files in your project to Git's staging area.

## Step 4: Create Your First Commit

```powershell
git commit -m "Initial commit: ETL Toll Traffic Airflow pipeline"
```

## Step 5: Connect to Your GitHub Repository

Replace `<your-username>` with your actual GitHub username:

```powershell
git remote add origin https://github.com/<your-username>/etl-toll-traffic-airflow.git
```

**Example**: If your username is `devis123`, the command would be:
```powershell
git remote add origin https://github.com/devis123/etl-toll-traffic-airflow.git
```

## Step 6: Rename Branch to Main (if needed)

```powershell
git branch -M main
```

## Step 7: Push to GitHub

```powershell
git push -u origin main
```

You'll be prompted for your GitHub username and password (or Personal Access Token).

**Note**: If you have 2FA enabled, you'll need to use a Personal Access Token instead of your password. You can create one at: GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)

## Step 8: Verify on GitHub

Go back to your GitHub repository page and refresh. You should see all your files there!

---

## Troubleshooting

### If you get "remote origin already exists" error:
```powershell
git remote remove origin
git remote add origin https://github.com/<your-username>/etl-toll-traffic-airflow.git
```

### If you need to update files later:
```powershell
git add .
git commit -m "Your commit message"
git push
```

### To check your remote URL:
```powershell
git remote -v
```
