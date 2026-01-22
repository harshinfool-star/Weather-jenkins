# Automating Jenkins Builds

## 🤖 Method 1: Git Webhooks (Instant Builds on Push)

### Setup with GitHub:
1. In your GitHub repo → Settings → Webhooks → Add webhook
2. Payload URL: `http://YOUR_JENKINS_URL:8080/github-webhook/`
3. Content type: `application/json`
4. Events: "Just the push event"
5. Save

### In Jenkins:
1. Job Configuration → Build Triggers
2. Check ✅ **"GitHub hook trigger for GITScm polling"**
3. Save

**Result**: Every time you `git push`, Jenkins automatically builds! 🚀

---

## 🔄 Method 2: SCM Polling (Check for Changes Periodically)

### In Jenkins Job Configuration:
1. Build Triggers → Check ✅ **"Poll SCM"**
2. Schedule (cron syntax):
   ```
   H/5 * * * *   # Check every 5 minutes
   H/15 * * * *  # Check every 15 minutes
   H * * * *     # Check every hour
   ```
3. Save

**Result**: Jenkins checks for new commits and builds if found.

---

## ⏰ Method 3: Scheduled Builds (Build at Specific Times)

### In Jenkins Job Configuration:
1. Build Triggers → Check ✅ **"Build periodically"**
2. Schedule:
   ```
   H 2 * * *       # Build daily at 2 AM
   H 2 * * 1-5     # Build weekdays at 2 AM
   H/30 * * * *    # Build every 30 minutes
   0 8,12,17 * * * # Build at 8 AM, 12 PM, 5 PM
   ```
3. Save

---

## 🎯 Recommended for Learning:

1. **Start**: Manual builds (what you're doing)
2. **Next**: Enable SCM polling (`H/5 * * * *`)
3. **Production**: Use GitHub webhooks for instant builds

---

## Cron Syntax Quick Reference:
```
* * * * *
│ │ │ │ │
│ │ │ │ └─── Day of week (0-7, Sun=0 or 7)
│ │ │ └───── Month (1-12)
│ │ └─────── Day of month (1-31)
│ └───────── Hour (0-23)
└─────────── Minute (0-59)

H = Hash (Jenkins distributes load automatically)
```

---

## 💡 Testing Auto-Build:

After enabling polling or webhooks:

```bash
# Make a change to index.html
echo "<!-- Test auto-build -->" >> index.html

# Commit and push
git add .
git commit -m "Test auto-build"
git push

# Jenkins will automatically detect and build! 🎉
```

Watch your Jenkins dashboard - you'll see a new build start automatically!
