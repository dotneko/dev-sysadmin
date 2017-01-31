- Functions provide additional capability and own functions can be defined.
- Scripts are usually saved as .ps1 files.
- Here is an example:

```
function add
{
    $add = [int](2+2)
    write-output $add
}
```

## Running Scripts in Powershell
```
.\Scriptname.ps1

```
## Define function(s) in a file and call it/them from the PowerShell commandline
```
. .\Scriptname.ps1
```
- Source and discussion: http://stackoverflow.com/questions/6016436/in-powershell-how-do-i-define-a-function-in-a-file-and-call-it-from-the-powersh

# Powershell script arguments

- [Powershell script arguments](http://stackoverflow.com/questions/2157554/how-to-handle-command-line-arguments-in-powershell)

# Comments in Powershell
```
# comment
<#
    Block comment
    Another comment in the block
#>
```

# Writing to the display
```
Write-Host "Some string"
Write-Host "Some string with $variable"
Write-Host Works even without the double-quotes
```

# Reading from input
```
$Variable = Read-Host -Prompt "Ask a question:"
```

### Example
```
$Server = Read-Host -Prompt 'Input your server name:'
$User = Read-Host -Prompt 'Input the user name:"
$Date = Get-Date
Write-Host "You input server '$Server' and '$User on '$Date'"
```

# While loop
- http://ss64.com/ps/while.html

# If statement
- http://www.computerperformance.co.uk/powershell/powershell_if_statement.htm

## Documenting functions
Format of comment based help:
```
function get-example {
    <#
    .SYNOPSIS
        A brief description of the function or script.

    .DESCRIPTION
        A longer description.

    .PARAMETER FirstParameter
        Description of each of the parameters

    .PARAMETER SecondParameter
        Description of each of the parameters

    .INPUTS
        Description of objects that can be piped to the script

    .OUTPUTS
        Description of objects that are output by the script

    .EXAMPLE
        Example of how to run the script

    .LINK
        Links to further documentation

    .NOTES
        Detail on what the script does, if this is needed

    #>
```
- Source: [PowerShell Practice and Style Documentation and Comments](https://github.com/PoshCode/PowerShellPracticeAndStyle/blob/master/Style%20Guide/Documentation%20and%20Comments.md)
