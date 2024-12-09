# PowerShell

Powershell is designed for task automation and configuration management. It combines a command-line interface and a scripting language built on the .NET framework. It is object-oriented so it can handle complex data types and interact with system components more effectively. Can support macOS and Linux.

Powershell commands are known as `cmdlets` (command-lets). They follow a Verb-Noun naming convention. The Noun specifies the object on which the action is performed.

## Basic Cmdlets

`Get-Command` - list all available cmdlets, functions, aliases, and scripts.

`Get-Command -CommandType "Function"` - filter commands by type function.

`Get-Help Get-Date` - provides detailed info about cmdlets.

`Get-Alias` - lists cmd.exe aliases.

`Find-Module` - allows to search for modules in online repositories.

`Install-Module` - download and install a module. and example is `Install-Module -Name "PowerShellGet"`.

## Navigating the File System and Working with Files

`Get-ChildItem` - lists the files and directories in a location specified with the `-PATH` parameter.

`Set-Location _location` - set directory to change to.

`New-Item -Path ".\captain-cabin\captain-wardrobe" -ItemType "Directory"` - create new item with file-path and file-type.

`Remove-Item -Path '\Users\username\file.txt` - remove item or dir.

`Copy-Item -Path .\Users\username\file.txt -Destination .\User\otheruser\newfile.txt` - copy file to location.

`Get-Content -Path ".\file.txt"` - read file contents.

## Piping, Filtering, and Sorting Data

`Get-ChildItem | Sort-Object Length` - get current dir objects and sort by size.

`Get-ChildItem | Where-Object -Property "Extension" -eq ".txt"` - filter objects.

`Get-ChildItem | Select-Object Name,Length` - select specific properties from objects or limit the number of objects returned.

`Get-ChildItem | Sort-Object Length -Descending | Select-Object -First 1` - pipe multiple items.

`Select-String -Path ".\captain-hat.txt" -Pattern "hat"` - searches for text patterns within files (similar to grep).

###### Comparison Operators in Powershell

`-eq` - equal to.

`-ne` - not equal to.

`-gt` - greater than.

`-ge` - greater than or equal to.

`-lt` - less than.

`-le` - less than or equal to.

`-like` - used to match a patern.

## System and Network Information

`Get-ComputerInfo` - retrieves comprehensive system information, including OS information, hardware specifications, BIOS details, and more.

`Get-LocalUser` - lists all the local user accounts on the system.

`Get-NetIPConfiguration` - provides detailed information about the network interfaces on a system, including IP Addresses, DNS servers, and gateway configurations.

`Get-NetIPAddress` - shows details fora ll IP addresses configured on the system.

## System Analysis

`Get-Process` - provides a detailed view of all currently running processes, including CPU and memory usage.

`Get-Service` - allows the retrieval of information about the status of services on teh machine.

`Get-NetTCPConnection` - displays current TCP connections.

`Get-FileHash` - generating file hashes.

## Scripting

`Invoke-Command` - for executing commands on remote systems.

## Other

`-ep Bypass -nop` - these flags disable PowerShell's usual restrictions, allowing scripts to run without interference from security settings or user profiles.

`DownloadFile` - method that pulls a file from a remote server.

`iex` - executes a script.

##
