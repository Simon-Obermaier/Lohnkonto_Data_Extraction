# Deploy to Railway - Simple Guide

## What's Ready

Your backend has **ONE configuration file**: `nixpacks.toml`

```toml
[phases.setup]
nixPkgs = ["python311", "openjdk17"]  # ✅ Python + Java

[phases.install]
cmds = ["pip install --no-cache-dir -r requirements.txt"]

[start]
cmd = "uvicorn api:app --host 0.0.0.0 --port $PORT"
```

All Docker files removed - no conflicts!

## Deploy Steps

### 1. Push to GitHub

```bash
cd backend
git add nixpacks.toml
git commit -m "Fix Railway deployment: Python + Java"
git push
```

### 2. Railway Auto-Deploys

Railway will automatically:
- ✅ Detect `nixpacks.toml`
- ✅ Install Python 3.11
- ✅ Install OpenJDK 17 (Java)
- ✅ Install Python dependencies
- ✅ Start the server

**Build time:** ~3-4 minutes

### 3. Verify Deployment

```bash
curl https://lohnkontodataextraction-production-6d82.up.railway.app/health
```

**Expected response:**
```json
{
  "status": "healthy",
  "template_exists": true,
  "java_installed": true,
  "java_version": "openjdk version \"17..."
}
```

## Environment Variables

Make sure these are set in Railway dashboard:

```env
TEMPLATE_PATH=template.xlsx
ALLOWED_ORIGINS=*
```

## If Build Fails

Check Railway logs for:

1. **"Installing nixPkgs: python311 openjdk17"** ✅
2. **"pip install -r requirements.txt"** ✅
3. **"uvicorn api:app"** ✅

If you see errors, the build log will show exactly what failed.

## Files in Backend

- ✅ `nixpacks.toml` - Railway configuration
- ✅ `api.py` - FastAPI application
- ✅ `jar_processor.py` - JAR processor service
- ✅ `Lohnkonten-1.0.0.jar` - Java application
- ✅ `template.xlsx` - Excel template
- ✅ `requirements.txt` - Python dependencies
- ✅ `Procfile` - Fallback start command

**No Docker files - clean and simple!**

## That's It!

Push and wait 3-4 minutes. Railway handles everything else.

---

**Status:** Ready to deploy! 🚀
