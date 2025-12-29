# MemoryReset - Quick Start Guide

Get MemoryReset up and running in 5 minutes!

---

## Step 1: Install .NET 8 Runtime (If Not Installed)

**Check if you already have it:**
1. Open Command Prompt
2. Type: `dotnet --version`
3. If you see `8.x.x`, skip to Step 2

**If you need to install:**
1. Go to: https://dotnet.microsoft.com/download/dotnet/8.0
2. Download: **.NET Desktop Runtime 8.0.x (x64)**
3. Run the installer
4. Restart your computer

---

## Step 2: Download MemoryReset

1. Download `MemoryReset.exe` (single-file, ~2-10 MB)
2. Save it to a permanent location (e.g., `C:\Program Files\MemoryReset\`)
3. **Do NOT run from Downloads folder** (use a permanent location)

---

## Step 3: First Launch

1. Right-click `MemoryReset.exe`
2. Select **"Run as Administrator"**
3. Click **"Yes"** on the UAC prompt
4. The main window will open

**Why Administrator?**
MemoryReset needs admin rights to modify process memory. This is the same requirement as Task Manager.

---

## Step 4: Test Manual Optimization

Let's try optimizing a process manually:

1. Click **"Refresh"** button (or press F5)
2. Find a memory-heavy process (e.g., Chrome, Edge, VS Code)
3. Click the checkbox next to it
4. Set **Compression Level** slider to **5**
5. Click **"Both (Recommended)"**
6. Watch the memory drop!

**Expected Results:**
- Idle processes: 40-60% memory reduction
- Active processes: 20-40% memory reduction

---

## Step 5: Set Up Automatic Monitoring

Let's create your first rule:

### Example: Auto-optimize Google Chrome

1. Go to the **"Rules"** tab
2. Click **"Add New Rule"**
3. Edit the new row:
   - **Process Name**: `chrome`
   - **Threshold (MB)**: `1000`
   - **Check Interval (s)**: `60`
   - **Trim WS**: ✓ (check it)
   - **Compress**: ✓ (check it)
   - **Level**: `5`
   - **Aggressive**: ✗ (leave unchecked)
   - **Enabled**: ✓ (check it)
4. Click **"Save Settings"**
5. Go back to **"Processes"** tab
6. Click **"Auto (Rules)"** in the toolbar
7. Status bar should show **"Monitoring: Active"**

**What happens now?**
Every 60 seconds, MemoryReset checks Chrome's memory. If it exceeds 1000 MB (1 GB), it will automatically optimize it.

---

## Step 6: Enable Run on Startup (Optional)

Want MemoryReset to start automatically with Windows?

1. Check the **"Run on Startup"** checkbox in the toolbar
2. Done!

Now MemoryReset will:
- Start when Windows boots
- Run in the background
- Automatically apply your rules

---

## Quick Reference

### Keyboard Shortcuts
| Shortcut | Action |
|----------|--------|
| `F5` | Refresh process list |
| `Ctrl+M` | Start/Stop monitoring |
| `Ctrl+B` | Optimize selected (Both) |
| `Ctrl+L` | Select All |

### Common Use Cases

#### Free RAM for Gaming
```
1. Click "Select All" (Ctrl+L)
2. Uncheck your game launcher
3. Set Compression Level: 5
4. Click "Both (Recommended)" (Ctrl+B)
```

#### Auto-optimize Web Browser
```
Rule:
- Process: chrome (or msedge, firefox)
- Threshold: 500-1000 MB
- Interval: 60s
- Trim WS: ✓
- Compress: ✓
- Level: 5
```

#### Limit Background Apps
```
Rule:
- Process: slack (or discord, spotify)
- Threshold: 300 MB
- Interval: 120s
- Aggressive: ✓
- Max WS: 150 MB
```

---

## Recommended First Rules

### For Most Users
```
Browser (Chrome/Edge):
- Threshold: 800 MB
- Interval: 60s
- Level: 5

VS Code / IDE:
- Threshold: 600 MB
- Interval: 120s
- Level: 5

Slack / Discord:
- Threshold: 300 MB
- Interval: 120s
- Level: 5
- Aggressive: ✓
- Max WS: 150 MB
```

### For Gamers
```
Discord:
- Threshold: 200 MB
- Interval: 60s
- Aggressive: ✓
- Max WS: 100 MB

Spotify:
- Threshold: 150 MB
- Interval: 180s
- Level: 5
```

### For Power Users
```
Everything:
- Threshold: 50 MB
- Interval: 300s
- Level: 4

Notepad++:
- Threshold: 100 MB
- Interval: 180s
- Level: 5
```

---

## Tips & Tricks

### How to Check if It's Working
1. Go to **"Logs"** tab
2. You should see messages like:
   - `"Monitoring started"`
   - `"Optimizing chrome.exe (PID 12345)"`
   - `"Memory reduced from 1200 MB to 450 MB"`

### How Much Memory Will I Save?
**Typical Results:**
- Background apps: 50-70% reduction
- Browsers (idle): 40-60% reduction
- Browsers (active): 20-30% reduction
- Games: Don't optimize (keep them running fast!)

### What NOT to Optimize
**Never optimize:**
- `System`
- `csrss`
- `services`
- `winlogon`
- Antivirus software
- Any process you don't recognize

**Why?** These are critical for Windows. Optimizing them can cause crashes or instability.

### Best Compression Level
**Use Level 5** for almost everything:
- Best memory savings
- Minimal performance impact
- Recommended by Windows

Only use Level 1-4 if you notice performance issues.

---

## Troubleshooting

### "Application won't start"
- Install .NET 8 Desktop Runtime
- Try running as Administrator

### "Access Denied" when optimizing
- Make sure you ran as Administrator
- Some processes (antivirus) are protected and can't be optimized

### "Rules aren't triggering"
- Check that rule is **Enabled** (checkbox)
- Make sure **"Auto (Rules)"** is active (status bar shows "Monitoring: Active")
- Verify process name matches exactly (case doesn't matter)
- Check **Logs** tab for error messages

### "Memory goes right back up"
This is normal for active processes. They need the memory for their work.
- Try using **Aggressive mode** with Max WS limit
- Increase check interval (e.g., 60s → 120s)
- Raise the threshold

---

## Next Steps

You're all set! Here's what to do next:

1. **Monitor the Logs tab** for the first hour to see what's happening
2. **Adjust your rules** based on what you see
3. **Export your rules** (Rules tab → Export Rules) as backup
4. **Read the full User Guide** (USER_GUIDE.md) for advanced features

---

## Support

- 📖 Full documentation: [USER_GUIDE.md](USER_GUIDE.md)
- 🐛 Issues: Check Logs tab for error messages
- 💡 Need help? Review the Troubleshooting section

---

**Congratulations! You're now optimizing your system memory like a pro!**

---

*Last Updated: December 29, 2025*
*Version: 1.0*
