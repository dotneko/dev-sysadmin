*Links:*
- [Table of Basic PowerShell Commands](https://blogs.technet.microsoft.com/heyscriptingguy/2015/06/11/table-of-basic-powershell-commands/)

---
- Everything is treated like an object, which could be configured and manipulated with PowerShell
- Object oriented, interactive shell that enables task automation and bulk operations.
- Based on the .NET framework
- Commands and arguments are *case-insensitive*.
- *Aliases* help to bridge gap between languages.

    E.g. `dir` is actually an alias for the PowerShell command `Get-Child`.

- Built into many products including 3rd party products.

# How to Read Powershell

```
Get-Service -name *net*         # Displays all services that contain net
Get-Service -name "*net*"       # Performs the same function
```

- `Get` is the **verb**, `Service` is the **noun**, while `Get-Service` is the **command**.
- `-name` is the **name**, `"*net*"` is the **argument**, while `-name "*net*"` is the **parameter**
- Parameters are like adjectives.
- Almost all commands are singular.

# Power of the Pipe

- The pipe operator: `|`
- Output from one command becomes input for the next.
- Also strings together multiple commands.
- Parameter binding is the key; "|" routes information to the correct command.


```
get-service|out-file c:\service.txt     # Pipes output from get-service into a text file
```

# Getting Help
- PowerShell Supports tab suggestions, e.g. Typing `Get-` and then <Tab> will offer suggestions.
- `help` is similar to `Get-Help` but also attaches the "More" function to it.
- `man` is an alias for `help`.
- *N.B. Help may need to be updated by* `Update-Help`

```
Get-Help <cmdlet name>
Get-Help <keyword>
```

### Getting Help: Examples

```
Get-Help alias                      # Get help entry for the command alias
Get-Help New-Alias
New-Alias -name "lsss" "Get-ChildItem"

Get-help get-service -examples      # Get help entry for get-service examples
Get-help get-service -online        # N.B. Requires a browser to display the online help
```

# Cmdlets and Aliases

```
Get-Command         # Gets all commands that are installed on the computer.
Get-Command|More
gcm                 # Alias for Get-Command

Get-ChildItem       # Powershell command for dir or ls; actually dir and ls are aliases of this command.
gci                 # Alias for Get-ChildItem

Alias               # Displays all aliases in the current environment
Get-Help about_Aliases
```

# Exploring Services

```
Get-Service         # Lists all services, including running and stopped services.
Get-Service|Where-Object {$_.status -eq "stopped"}      # Search servies for Status "stopped"

Get-Member          # Gets the properties and methods of objects
```

- `Get-Service` can be piped into `Get-Member` so show the properties and methods of `Get-Service`.

```
Get-Service|Get-Member
```

# Exploring Local Users

```
Get-CIMinstance win32_useraccount
getWMIObject win32_useraccount
```
- Source and more info: [Find Local User Accounts Using PowerShell](https://www.petri.com/find-local-user-accounts-using-powershell)
