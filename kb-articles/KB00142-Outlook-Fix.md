# KB00142: Outlook Desktop Client Profile Corruption Remediation

## Symptoms
* Desktop client hangs indefinitely on the "Loading Profile..." splash screen.
* Continuous prompting for credentials despite entering valid inputs.

## Standard Operating Procedure (SOP)
1. Close all Office processes via PowerShell:
```powershell
   Stop-Process -Name "outlook" -Force
```
2. Open the Run dialog (`Win + R`), type `outlook.exe /safe`, and hit Enter.

3. If Safe Mode works, disable third-party add-ins under File > Options > Add-ins.

4. If Safe Mode fails, navigate to Windows Control Panel > Mail > Show Profiles.

5. Delete the corrupted profile, navigate to `%localappdata%\Microsoft\Outlook\`, and delete the `.ost` cache file.

6. Create a new profile named `M365-Primary`, enter the user's email, and relaunch Outlook to trigger a fresh cloud mailbox download.
