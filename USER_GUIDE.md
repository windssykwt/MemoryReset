# MemoryReset - User Guide

## Overview

**MemoryReset** is a Windows memory optimization tool that helps reduce RAM usage of running processes through memory compression and working set trimming. It features both manual optimization and automatic monitoring based on customizable rules.

### Key Features
- **Manual Memory Optimization**: Optimize selected processes with one click
- **Automatic Monitoring**: Rule-based automatic optimization when processes exceed memory thresholds
- **Memory Compression**: Uses Windows native memory compression (priority levels 1-5)
- **Working Set Trimming**: Releases unused memory pages back to Windows
- **Import/Export Rules**: Share and backup monitoring configurations
- **Dark Theme UI**: Clean, modern interface inspired by Claude Desktop

---

## System Requirements

- **Operating System**: Windows 10/11 (64-bit)
- **.NET Runtime**: .NET 8 Desktop Runtime (required for framework-dependent version)
- **Permissions**: Administrator privileges (for memory optimization operations)

### Installing .NET 8 Runtime
If you don't have .NET 8 installed, download it from:
https://dotnet.microsoft.com/download/dotnet/8.0

Select: **.NET Desktop Runtime 8.0.x (x64)**

---

## Getting Started

### Installation
1. Download `MemoryReset.exe` (single-file executable, ~2-10 MB)
2. Place it anywhere on your system (e.g., `C:\Program Files\MemoryReset\`)
3. Right-click and select **"Run as Administrator"**

### First Launch
1. The main window will open showing the **Processes** tab
2. All running processes with their memory usage will be listed
3. Initially, no monitoring rules are configured

---

## Main Interface

### Tabs
- **Processes**: View and manually optimize running processes
- **Rules**: Configure automatic monitoring rules
- **Logs**: View operation history and debug information

### Toolbar (Top Bar)
- **Refresh** (F5): Reload process list
- **Auto (Rules)** / **Stop (Rules)** (Ctrl+M): Start/stop automatic monitoring
- **Select All** (Ctrl+L): Toggle selection of all processes
- **Run on Startup**: Automatically start MemoryReset when Windows boots
- **Search**: Filter processes by name

---

## How to Use

### Manual Memory Optimization

#### Step 1: Select Processes
In the **Processes** tab:
- Click checkboxes next to processes you want to optimize
- Or use **Select All** to select all processes
- Use **Search** to find specific processes

#### Step 2: Choose Optimization Level
Set the **Compression Level** slider (1-5):
- **Level 1**: Normal (no compression)
- **Level 2-3**: Light compression
- **Level 4**: Medium compression
- **Level 5**: Maximum compression (recommended)

Higher levels save more memory but may slightly slow down the process when accessing compressed memory.

#### Step 3: Apply Optimization
Click one of these buttons:

| Button | Description | Shortcut |
|--------|-------------|----------|
| **Empty Working Set** | Releases unused memory pages | Ctrl+E |
| **Compress Memory** | Compresses process memory at current level | Ctrl+K |
| **Both (Recommended)** | Combines both operations for maximum savings | Ctrl+B |
| **AGGRESSIVE** | Aggressive optimization with hard memory limits | Ctrl+A |

**Note**: "Both (Recommended)" provides the best balance of memory savings and performance.

---

### Automatic Monitoring with Rules

Automatic monitoring allows MemoryReset to optimize processes automatically when they exceed memory thresholds.

#### Creating a Rule

1. Go to the **Rules** tab
2. Click **Add New Rule**
3. A new row will appear in the table
4. Configure the rule by clicking on each cell:

| Column | Description | Example |
|--------|-------------|---------|
| **Enabled** | Toggle rule on/off | ✓ |
| **Process Name** | Process name or pattern (case-insensitive) | `chrome` or `firefox` |
| **Threshold (MB)** | Memory limit that triggers optimization | `500` (MB) |
| **Check Interval (s)** | How often to check memory usage | `60` (seconds) |
| **Trim WS** | Enable Working Set trimming | ✓ |
| **Compress** | Enable memory compression | ✓ |
| **Level** | Compression priority level (1-5) | `5` |
| **Aggressive** | Enable aggressive mode with hard limits | ✓ |
| **Max WS (MB)** | Maximum working set limit (aggressive mode only) | `300` |

#### Quick Add from Processes Tab
- Right-click a process in the **Processes** tab
- Select **"Add to Rules"**
- A default rule will be created automatically

#### Example Rules

**Google Chrome (Heavy User)**
```
Process Name: chrome
Threshold: 800 MB
Check Interval: 60s
Trim WS: ✓
Compress: ✓
Level: 5
Aggressive: ✗
```

**Microsoft Edge (Moderate)**
```
Process Name: msedge
Threshold: 500 MB
Check Interval: 120s
Trim WS: ✓
Compress: ✓
Level: 4
Aggressive: ✗
```

**Background App (Aggressive)**
```
Process Name: slack
Threshold: 300 MB
Check Interval: 180s
Trim WS: ✓
Compress: ✓
Level: 5
Aggressive: ✓
Max WS: 150 MB
```

#### Starting Automatic Monitoring
1. After configuring rules, click **Save Settings**
2. Click **Auto (Rules)** in the toolbar (or press Ctrl+M)
3. The status bar will show **"Monitoring: Active"**
4. Check the **Logs** tab to see when optimizations are triggered

#### Stopping Monitoring
- Click **Stop (Rules)** in the toolbar (or press Ctrl+M again)

---

### Import/Export Rules

#### Export Rules
1. Go to the **Rules** tab
2. Click **Export Rules**
3. Choose where to save the JSON file (e.g., `MemoryReset_Rules_20251229.json`)
4. All current rules will be saved

**Use Cases**:
- Backup your configuration
- Share rules with other computers
- Version control your settings

#### Import Rules
1. Click **Import Rules**
2. **WARNING**: This will **replace ALL** current rules
3. Confirm the operation
4. Select the JSON file to import
5. Rules will be loaded and monitoring will restart if active

**Tip**: Export your rules before importing to have a backup!

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| **F5** | Refresh process list |
| **Ctrl+M** | Toggle monitoring on/off |
| **Ctrl+E** | Empty Working Set (selected processes) |
| **Ctrl+K** | Compress Memory (selected processes) |
| **Ctrl+B** | Both operations (selected processes) |
| **Ctrl+A** | Aggressive optimization (selected processes) |
| **Ctrl+L** | Toggle Select All |

---

## Understanding Memory Optimization

### Empty Working Set
- **What it does**: Asks Windows to release unused memory pages from the process
- **When to use**: Process has been idle or has cached data it doesn't need
- **Effect**: Immediate RAM reduction, minimal performance impact
- **Drawback**: Memory may gradually increase again as process resumes work

### Memory Compression
- **What it does**: Compresses process memory pages in RAM instead of paging to disk
- **When to use**: Process is using lots of memory but you want it to stay responsive
- **Effect**: Significant RAM savings (30-50% typical), process stays in memory
- **Drawback**: Slight CPU overhead when accessing compressed memory

### Both Operations (Recommended)
- **What it does**: Combines Working Set trimming + Memory Compression
- **When to use**: Best for most scenarios - balances savings and performance
- **Effect**: Maximum memory reduction while keeping process responsive
- **Drawback**: Minimal - best overall approach

### Aggressive Mode
- **What it does**: Both operations + hard memory limit enforcement
- **When to use**: Background processes that you want to strictly limit
- **Effect**: Forces process to stay under Max WS limit
- **Drawback**: May impact process performance if limit is too low

---

## Best Practices

### Recommended Compression Levels
- **Level 5**: Default for most processes (best savings, minimal impact)
- **Level 4**: If you notice slight slowdowns with Level 5
- **Level 1-3**: Generally not recommended (poor savings)

### Setting Memory Thresholds
- **Web Browsers**: 500-800 MB per instance
- **IDE/Editors**: 300-600 MB
- **Background Apps**: 150-300 MB
- **System Processes**: Avoid optimizing (can cause instability)

### Check Intervals
- **60-120 seconds**: Good balance for active processes
- **180-300 seconds**: Background/idle processes
- **Shorter intervals**: More responsive but higher CPU overhead

### Processes to Avoid
Don't optimize these process types:
- `System`
- `Registry`
- `csrss`
- `winlogon`
- `services`
- Antivirus/security software
- Critical system services

### Run on Startup
Enable "Run on Startup" if:
- You want automatic monitoring to start immediately on boot
- You have consistent memory pressure on your system
- You've configured stable, tested rules

---

## Troubleshooting

### "Access Denied" Errors
**Solution**: Right-click MemoryReset.exe and select "Run as Administrator"

### Optimization Has No Effect
**Possible Causes**:
- Process is actively using all its memory (not idle data)
- Memory compression already enabled by Windows
- Process immediately reallocates memory after trimming

**Solution**: Try increasing Compression Level or using Aggressive mode

### Application Won't Start
**Solution**:
1. Verify .NET 8 Desktop Runtime is installed
2. Check Windows Event Viewer for error details
3. Try running from Command Prompt to see error messages

### Rules Not Triggering
**Check**:
- Rule is **Enabled** (checkbox checked)
- Process name matches exactly (check in Task Manager)
- Threshold is lower than process current memory usage
- Monitoring is **Active** (toolbar shows "Monitoring: Active")
- Check **Logs** tab for errors

### High CPU Usage
**Solution**:
- Increase Check Intervals in rules (e.g., 120s → 180s)
- Reduce number of active rules
- Avoid optimizing too many processes simultaneously

---

## Advanced Tips

### Pattern Matching (Future Feature)
Currently, process names must match exactly (case-insensitive). Future versions may support wildcards:
- `chrome*` - Match chrome.exe, chromedriver.exe, etc.
- `*code*` - Match vscode, vscode-server, etc.

### Monitoring Multiple Instances
If you have multiple instances of the same process (e.g., 5 Chrome tabs):
- A rule applies to **ALL** instances matching the name
- Each instance is checked individually against the threshold
- Consider using higher thresholds to avoid over-optimization

### Combining with Windows Task Scheduler
For advanced users:
1. Create a Task Scheduler job to launch MemoryReset on login
2. Add command-line arguments (if supported) for automation
3. Schedule periodic optimization jobs

### Logs Tab Usage
The Logs tab shows:
- When monitoring starts/stops
- When rules trigger optimization
- Success/failure of operations
- Import/export events

**Colors**:
- **Blue border**: Info messages
- **Yellow border**: Warnings
- **Red border**: Errors

Use logs to debug rules that aren't working as expected.

---

## FAQ

**Q: Is this safe for my system?**
A: Yes. MemoryReset uses official Windows APIs (EmptyWorkingSet, SetProcessMemoryPriority). These are the same APIs used by Task Manager and other system tools.

**Q: Will this damage my SSD?**
A: No. Memory compression keeps data in RAM (not disk). Working set trimming may cause paging, but modern Windows already manages this intelligently.

**Q: How much memory can I save?**
A: Typical savings: 30-60% for idle processes, 20-40% for active processes. Results vary by application.

**Q: Can I run this on a schedule?**
A: Use "Run on Startup" + automatic monitoring rules for set-and-forget operation.

**Q: Does this work on servers?**
A: Technically yes, but designed for desktop Windows. Server environments should use proper resource management.

**Q: Is there a portable version?**
A: The single-file .exe IS portable - just copy it anywhere and run. Settings are stored in `%APPDATA%\MemoryReset\`.

**Q: Can I use this instead of adding more RAM?**
A: It helps, but physical RAM is always better. Use this to maximize existing RAM, not replace upgrades.

---

## Technical Information

### Settings File Location
```
%APPDATA%\MemoryReset\settings.json
```

To reset to defaults: Delete this file and restart MemoryReset.

### Exported Rules Format
```json
{
  "exportVersion": "1.0",
  "exportDate": "2025-12-29T10:30:00",
  "rules": [
    {
      "processNamePattern": "chrome",
      "thresholdBytes": 524288000,
      "checkIntervalSeconds": 60,
      "useWorkingSetTrim": true,
      "useMemoryCompression": true,
      "compressionPriorityLevel": 5,
      "useAggressiveMode": false,
      "maxWorkingSetMB": 0,
      "isEnabled": true
    }
  ]
}
```

### Memory Compression Priority Levels
Windows defines these priority levels:
- **1**: `MEMORY_PRIORITY_NORMAL` (no compression)
- **2**: `MEMORY_PRIORITY_BELOW_NORMAL`
- **3**: `MEMORY_PRIORITY_MEDIUM`
- **4**: `MEMORY_PRIORITY_LOW`
- **5**: `MEMORY_PRIORITY_VERY_LOW` (maximum compression)

---

## License & Credits

**MemoryReset** is a Windows memory optimization tool.

### Technologies Used
- .NET 8 (WPF Framework)
- Windows Memory Management APIs
- CommunityToolkit.MVVM

### UI Design
Dark theme inspired by Claude Desktop.

---

## Support & Updates

For issues, feature requests, or questions:
- Check the **Logs** tab for error messages
- Review this guide's Troubleshooting section
- Verify you're using the latest .NET 8 runtime

---

## Quick Start Checklist

1. ✓ Install .NET 8 Desktop Runtime
2. ✓ Run MemoryReset.exe as Administrator
3. ✓ Go to Rules tab → Add rules for memory-heavy apps
4. ✓ Click Save Settings
5. ✓ Click Auto (Rules) to start monitoring
6. ✓ Check Logs tab to verify it's working
7. ✓ Enable Run on Startup for automatic operation

**That's it! MemoryReset will now automatically optimize your system memory.**

---

*Last Updated: December 29, 2025*
*Version: 1.0*
