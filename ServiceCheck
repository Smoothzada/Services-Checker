param ()
$ErrorActionPreference = "SilentlyContinue"
$global:ReturnData = @()

class Service {
    [string]$Name           = ""
    [string]$DisplayName    = ""
    [string]$State          = ""
    [string]$PathName       = ""
    [string]$Bannable       = "Não"
}

$BannableServices = @('dusmvc', 'appinfo', 'wsearch', 'DPS', 'pcasvc', 'eventlog', 'sysmain', 'msmpeng', 'dusmsvc')

function Get-ServiceDetailed {
    [CmdletBinding()]
    param ([Parameter(Mandatory=$true)][array]$Services)

    foreach($Service in $Services) {
        $NewService = [Service]::new()
        $NewService.Name        = $Service.Name
        $NewService.DisplayName = $Service.DisplayName
        $NewService.State       = $Service.State
        $NewService.PathName    = $Service.PathName

        if ($BannableServices -contains $Service.Name.ToLower()) {
            $NewService.Bannable = "Sim"
        }

        $global:ReturnData += $NewService
    }
}

$AllServices = Get-WmiObject win32_service | select Name, DisplayName, State, PathName 

Get-ServiceDetailed -Services $AllServices

$global:ReturnData | Out-GridView

Return $global:ReturnData
