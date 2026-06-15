# KB00195: OneDrive for Business Sync Engine Reset Playbook

## Symptoms
* Red "X" overlay icons appearing on local file paths in File Explorer.
* OneDrive status stuck on "Processing changes" with zero data data transfer.

## Standard Operating Procedure (SOP)
1. Search the Windows Start Menu for "Credential Manager" and select Windows Credentials.
2. Scroll to Generic Credentials and remove all entries starting with `MicrosoftOffice16_Data`.
3. Open the Run dialog (`Win + R`).
4. Execute the application reset command:
```PowerShell
   %localappdata%\Microsoft\OneDrive\onedrive.exe /reset
```
- Wait 60 seconds. If the cloud icon does not reappear in the system tray, manually relaunch it by running:
``` PowerShell
   %localappdata%\Microsoft\OneDrive\onedrive.exe
```
