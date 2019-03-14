# Instructions

Tested on:
- Windows Server 2016 Standard Edition build 14393

To create a new self-signed certificate:

    New-SelfSignedCertificate -CertStoreLocation Cert:\LocalMachine\My -DnsName
"$env:computername" -FriendlyName "WinRM HTTPS Certificate" -NotAfter (Get-
Date).AddYears(5)

To set up a new listener:

    New-Item -Path WSMan:\Localhost\Listener -Transport HTTPS -Address * -
CertificateThumbprint <thumbprint of certificate>

To open the firewall for WinRM over HTTPS:

    New-NetFirewallRule -DisplayName 'WinRM HTTPS Management' -Profile
Domain,Private -Direction Inbound -Action Allow -Protocol TCP -LocalPort
5986

To enable Basic Authentication for WinRM:

    Set-Item -Path "WSMan:\localhost\Service\Auth\Basic" -Value $true

Alternatively, to use the ready-made script from Ansible for this purpose:

    $ansibleconfigurl = "https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1"
    $ansibleconfig = "$env:temp\ConfigureRemotingForAnsible.ps1"
    (New-Object -TypeName System.Net.WebClient).DownloadFile($ansibleconfigurl,$ansibleconfig)
    powershell.exe -ExecutionPolicy ByPass -File $ansibleconfig
