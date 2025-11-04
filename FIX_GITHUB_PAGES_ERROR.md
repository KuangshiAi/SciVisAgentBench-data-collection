# Fix GitHub Pages "Not Found" Error

## What Happened?

You're seeing this error:
```
Error: Get Pages site failed. Please verify that the repository has Pages enabled
Error: HttpError: Not Found
```

This happens because GitHub Actions is trying to deploy, but GitHub Pages isn't configured correctly.

## Quick Fix (3 minutes)

### Step 1: Remove the GitHub Actions Workflow

The `.github/workflows/` folder has been removed from your project. Now commit this change:

```bash
cd /Users/kuangshiai/Documents/ND-VIS/SciVisAgentBench-data_collection_page

# Stage the deletion
git add -A

# Commit
git commit -m "Remove GitHub Actions workflow - use simple Pages deployment"

# Push to GitHub
git push
```

### Step 2: Configure GitHub Pages Correctly

1. **Go to your repository on GitHub**:
   ```
   https://github.com/YOUR_USERNAME/SciVisAgentBench-data-collection
   ```

2. **Click "Settings"** tab (top of page)

3. **Click "Pages"** in the left sidebar

4. **Under "Build and deployment"**:
   - **Source**: Select **"Deploy from a branch"** ⬅️ IMPORTANT!
   - **Branch**: Select **"main"** and **"/ (root)"**
   - Click **"Save"**

5. **Wait 2 minutes** and refresh the page

6. **You should see**:
   ```
   Your site is live at https://YOUR_USERNAME.github.io/SciVisAgentBench-data-collection/
   ```

### Step 3: Verify It Works

Visit your site:
```
https://YOUR_USERNAME.github.io/SciVisAgentBench-data-collection/
```

Should work now! ✅

---

## Why Did This Happen?

Your project had a `.github/workflows/deploy.yml` file that was trying to use GitHub Actions to deploy. This requires special configuration. For simple projects, it's easier to use "Deploy from a branch" instead.

---

## Two Deployment Methods

### Method 1: Deploy from Branch (Simpler) ✅ ← We're using this

**Pros:**
- No configuration needed
- Just push to main branch
- Automatic deployment

**Setup:**
- Settings → Pages → Source: "Deploy from a branch"

### Method 2: GitHub Actions (More Complex)

**Pros:**
- Can run build steps
- More control
- Custom workflows

**Setup:**
- Settings → Pages → Source: "GitHub Actions"
- Need properly configured workflow file

---

## If You Still See Errors

### Error: "404 - File not found"

**Check:**
1. Is `index.html` in the root of your repository?
   ```bash
   ls index.html
   # Should show: index.html
   ```

2. Did you push all files?
   ```bash
   git status
   # Should show: "nothing to commit, working tree clean"
   ```

3. Is repository public?
   - Repo Settings → General → Danger Zone
   - Should say "Public"

### Error: "Site not found"

**Solution:** Wait 2-3 minutes after configuring Pages, then refresh.

### Error: Actions workflow still running

**Solution:**
1. Go to "Actions" tab in your repo
2. Click the running workflow
3. Click "Cancel workflow" (top right)
4. Workflow file has been removed, won't happen again

---

## Verify Your Setup

Run these checks:

```bash
cd /Users/kuangshiai/Documents/ND-VIS/SciVisAgentBench-data_collection_page

# Check workflow is gone
ls .github/workflows/
# Should show: "No such file or directory" ✅

# Check all files are committed
git status
# Should show: "nothing to commit" ✅

# Check remote is set
git remote -v
# Should show your GitHub URL ✅
```

---

## Complete Command Summary

If you need to redo everything:

```bash
# 1. Remove workflow (already done)
# 2. Commit and push
cd /Users/kuangshiai/Documents/ND-VIS/SciVisAgentBench-data_collection_page
git add -A
git commit -m "Remove GitHub Actions workflow"
git push

# 3. Configure on GitHub:
#    Settings → Pages → Source: "Deploy from a branch"
#    Branch: "main", folder: "/ (root)"

# 4. Wait 2 minutes and visit:
#    https://YOUR_USERNAME.github.io/SciVisAgentBench-data-collection/
```

---

## Success Criteria

✅ No errors in GitHub Actions tab
✅ Settings → Pages shows "Your site is live at..."
✅ Visiting the URL shows your website
✅ Can navigate between pages

---

## Need More Help?

**Check GitHub Pages Status:**
- Repo Settings → Pages
- Should show: "Your site is live at..." (green checkmark)

**Check Repository:**
- Make sure it's Public (required for free Pages)
- Make sure `index.html` exists in root
- Make sure all files are pushed

**Still stuck?**
1. Take a screenshot of the error
2. Take a screenshot of Settings → Pages
3. Open an issue with these screenshots

---

## What's Next?

After your site is live:

1. ✅ Test all pages work
2. ✅ Test form submission (demo mode)
3. 🔥 Add Firebase for cloud storage (optional)

Follow `FIREBASE_QUICKSTART.md` when ready!
