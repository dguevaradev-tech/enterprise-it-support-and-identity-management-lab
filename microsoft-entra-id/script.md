``` Powershell
# 1. Credentials and Silent Connection
$TenantID     = "dguevaratechoutlook…”
$ClientID     = "YOUR_SECRET_HERE"
$ClientSecret = "YOUR_SECRET_HERE"

 $SecretSecure = ConvertTo-SecureString $ClientSecret -AsPlainText -Force
 $AppCredential = New-Object System.Management.Automation.PSCredential($ClientID, $SecretSecure)
 Connect-MgGraph -Credential $AppCredential -TenantId $TenantID -NoWelcome

 # 2. Grab the clean CSV.
 $CSVPath = "C:\Users\dguev\Documents\users.csv"
 $Users = Import-Csv -Path $CSVPath

 # 3. Loop and Provision using Splatting
 foreach ($User in $Users) {
     $First = $User.FirstName
     $Last  = $User.LastName
     $Dept  = $User.Department
     $Title = $User.Title
     $SAM   = ($First[0] + $Last).ToLower()
     $UPN   = "$SAM@$TenantID"

     $PasswordProfile = @{
         Password = “HIDDENPASSWORD”
         ForceChangePasswordNextSignIn = $true
     }

     $UserParams = @{
         DisplayName       = "$First $Last"
         GivenName         = $First
         Surname           = $Last
         UserPrincipalName = $UPN
         MailNickName      = $SAM
         AccountEnabled    = $true
         PasswordProfile   = $PasswordProfile
         Department        = $Dept
         JobTitle          = $Title
     }

     # Execute User Creation
     $NewUser = New-MgUser @UserParams

     if ($NewUser.Id) {
         Write-Host "SUCCESS: Fully Provisioned $UPN" -ForegroundColor Cyan
     } else {
         Write-Host "FAILED: Could not create $UPN" -ForegroundColor Red
     }}
```
