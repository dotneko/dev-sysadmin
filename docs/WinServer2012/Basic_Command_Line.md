*References and Links:*
- [Command Line Reference](https://commandwindows.com/command3.htm)

### CMD commands
```
cls         # clear commandline
help        # list DOS commands
dir
dir *.exe /s
find
findstr
netdom
shutdown
powershell  # enters powershell environment
```

# Network Commands
```
ipconfig
netstat
nslookup
```

# NET services
```
net
net help
net command ?       # displays syntax of the command
net computer
net localgroup      # equivalent to bash-$ getent groups
net use             # allows connection to another network; shows network shares
net view            
```

# Changing Computer Name
```
netdom renamecomputer compname /newname:a_New_Name
wmic computersystem where caption='currentname' rename newname
```

# Changing the Time/Date/Timezone
```
date                                # Displays current date and time
tzutil
tzutil /l                           # Lists valid timezones
tzutil /l|findstr /R /C:"Canada"    # Filters list of timezones for "Canada" (case sensitive)
tzutil /l|findstr /R /I /C:"canada" # Use /I for a non-case-sensitive search.
tzutil /l|Select-String canada      # Filters list of timezones for "canada" (PowerShell)

```

# Windows Core Server Configuration Screen
```
sconfig
```
