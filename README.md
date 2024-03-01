# Uninstall Teams PowerShell Script
This PowerShell script is designed to uninstall Microsoft Teams from a Windows machine, targeting both the per-user installation and the machine-wide installer. It also removes any Teams app packages for all users and any provisioned Teams app packages from the system.

## Customizing Team Paths
If you have Teams installed in a non-standard location, you can add custom paths to the `$TeamsPaths` array within the script. This ensures that the script targets all relevant installations on your system.

To add a custom path, locate the $TeamsPaths array definition in the script and append your custom path as follows:

```powershell
$TeamsPaths = @(
  (Get-ChildItem -Path "C:\Users\*\AppData\Local\Microsoft\Teams").FullName,
  "C:\Custom\Path\To\Teams"
)
```
Replace "C:\Custom\Path\To\Teams" with the actual path to your Teams installation. You can add as many custom paths as necessary by appending more lines in the same format. The path should be to where `Update.exe` is located.

## Usage Instructions
To automate the deployment of this script across multiple systems using SCCM, follow these steps:

1. **Create a New Package**: In the SCCM console, navigate to the Software Library, create a new package, and specify the script file as the source.

2. **Create a Program for the Package**: Define a program for the package, setting the command line to execute the PowerShell script. Use the command:
  ```powershell
  PowerShell.exe -ExecutionPolicy Bypass -File "path\to\UninstallTeams.ps1"
  ```
  Replace `"path\to\UninstallTeams.ps1"` with the actual path to your script within the package source location.

3. **Deploy the Package**: Assign the package to a collection of computers where Teams needs to be uninstalled. Set the deployment settings according to your organization's requirements.

## Disclaimer
This script is provided as-is, without warranty of any kind. Use of this script is at your own risk. Always ensure you have backups of important data before running scripts that affect system configurations and installed applications.

## Contributing
Feedback and contributions to improve this script are welcome. Please feel free to fork the repository, make your changes, and submit a pull request.