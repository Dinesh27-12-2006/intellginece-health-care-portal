# Vercel Deployment Fix

## The Error You're Seeing

```
invalid request: should NOT have additional property 'public'. Please remove it.
```

## How to Fix

### Option 1: Fix in Vercel UI (Easiest)

1. **Clear the Root Directory field**
   - In the Vercel deployment screen, find "Root Directory"
   - Clear the field completely (leave it empty)
   - Or change `./` to just `.` (dot without slash)

2. **Keep these settings:**
   - Framework Preset: **Other**
   - Build Command: Leave empty
   - Output Directory: Leave empty
   - Install Command: Leave empty

3. **Click Deploy Again**

### Option 2: Use Updated vercel.json

The `vercel.json` file has been simplified. Make sure you have the latest version:

```bash
git pull origin main
```

Then try deploying again.

## Why This Happened

Your HTML files (`index.html`, `login.html`, etc.) are in the root directory of your repository, not in a subdirectory. Vercel was looking for them in the wrong place.

## Correct Vercel Configuration

```
Root Directory: (empty or ".")
Framework: Other
Build Command: (none)
Output Directory: (none)
```

## Alternative: Use Vercel CLI

If the UI keeps giving you issues, deploy via CLI:

```bash
# Install Vercel CLI (if not already installed)
npm install -g vercel

# Login
vercel login

# Deploy (from your project directory)
vercel --prod

# It will ask you questions - answer:
# Set up and deploy? Y
# Which scope? Choose your account
# Link to existing project? N
# Project name? intellginece-health-care-portal
# Directory? ./ (or just press Enter)
# Override settings? N
```

## Verification

After successful deployment, test:
1. Visit your deployment URL
2. You should see the landing page (index.html)
3. Click "Get Started" - should go to login page
4. Signup should work (after adding Supabase credentials)

## Still Having Issues?

The error message suggests there might be a configuration in the Vercel UI that's conflicting. Try:

1. Delete the project from Vercel
2. Create a new project
3. Import from GitHub again
4. Don't touch Root Directory (leave it empty)
5. Add your environment variables
6. Deploy

## Need Help?

Check the main deployment guide: `DEPLOYMENT.md`
