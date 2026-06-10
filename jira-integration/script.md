```
# 1. Environment & Authentication Variables
$SiteUrl     = "https://WORKSPACENAME.atlassian.net/"
$ServiceDeskId = “#”
$ProjectKey  = “ABCD”
$UserEmail   = “your@email.com"
$ApiToken    = “LONGTOKEN#############################”

# Convert credentials into standard Base64 Authorization headers
$AuthString  = "${UserEmail}:${ApiToken}"
$AuthBytes   = [System.Text.Encoding]::UTF8.GetBytes($AuthString)
$Base64Auth  = [System.Convert]::ToBase64String($AuthBytes)
$Headers     = @{
    "Authorization" = "Basic $Base64Auth"
    "Content-Type"  = "application/json"
}

$Incidents = @(
    @{
        Summary     = "Account Lockout / Expired Temporary Password - User: nalbright"
        Description = "User Noah Albright (nalbright@dguevaratechoutlook.onmicrosoft.com) from Human Resources (Talent Acquisition Specialist) reports being unable to complete his initial cloud login phase using temporary credential profile. Throws password expiration fault loop. Requires manual administrative directory override."
    },
    @{
        Summary     = "Account Lockout / Expired Temporary Password - User: egallagher"
        Description = "User Emma Gallagher (egallagher@dguevaratechoutlook.onmicrosoft.com) from Finance (Financial Analyst) reports being unable to complete her initial cloud login phase using temporary credential profile. Throws password expiration fault loop. Requires manual administrative directory override."
    },
    @{
        Summary     = "Account Lockout / Expired Temporary Password - User: jromero"
        Description = "User Jackson Romero (jromero@dguevaratechoutlook.onmicrosoft.com) from Operations (Supply Chain Coordinator) reports being unable to complete his initial cloud login phase using temporary credential profile. Throws password expiration fault loop. Requires manual administrative directory override."
    }
)

# 3. Stream Engine Loop - Pushing Payloads to Jira REST API
foreach ($Incident in $Incidents) {
    
    # Universal Fallback JSON Payload
    $JsonPayload = @{
        fields = @{
            project   = @{ key = $ProjectKey }
            summary   = $Incident.Summary
            description = $Incident.Description
            issuetype = @{ name = "Task" }
        }
    } | ConvertTo-Json -Depth 10

    # Execute the API REST call
    $ApiEndpoint = "$SiteUrl/rest/api/2/issue"
    try {
        $Response = Invoke-RestMethod -Method Post -Uri $ApiEndpoint -Headers $Headers -Body $JsonPayload
        Write-Host "SUCCESS: Generated Ticket [$($Response.key)] - $($Incident.Summary)" -ForegroundColor Green
    } catch {
        $ErrorResponse = $_.Exception.Response
        if ($ErrorResponse) {
            $StreamReader = New-Object System.IO.StreamReader($ErrorResponse.GetResponseStream())
            $DetailedError = $StreamReader.ReadToEnd()
            Write-Host "FAILED: Jira Rejected Data. Reason: $DetailedError" -ForegroundColor Red
        } else {
            Write-Host "FAILED to inject ticket. Error context: $_" -ForegroundColor Red
        }
    }
}

```
