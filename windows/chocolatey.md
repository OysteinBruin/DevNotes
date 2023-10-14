## Chocolatey
[Chocolatey](https://chocolatey.org) is software management automation for Windows that wraps installers, executables, zips, and scripts into compiled packages.

---
### Installation

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

- Verify installation:

```powershell
choco -?
```
should display a listing of available commands

---
### Usage

```powershell
choco install <package>
```