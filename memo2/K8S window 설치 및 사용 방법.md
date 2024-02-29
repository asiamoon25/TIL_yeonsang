# window

### chocolatey 설치

관리자 권한의 powershell 실행

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
해당 명령어 실행

```powershell
Forcing web requests to allow TLS v1.2 (Required for requests to Chocolatey.org)
Getting latest version of the Chocolatey package for download.
Not using proxy.
Getting Chocolatey from https://community.chocolatey.org/api/v2/package/chocolatey/2.2.2.
Downloading https://community.chocolatey.org/api/v2/package/chocolatey/2.2.2 to C:\Users\happy\AppData\Local\Temp\chocolatey\chocoInstall\chocolatey.zip
Not using proxy.
Extracting C:\Users\happy\AppData\Local\Temp\chocolatey\chocoInstall\chocolatey.zip to C:\Users\happy\AppData\Local\Temp\chocolatey\chocoInstall
Installing Chocolatey on the local machine
Creating ChocolateyInstall as an environment variable (targeting 'Machine')
  Setting ChocolateyInstall to 'C:\ProgramData\chocolatey'
WARNING: It's very likely you will need to close and reopen your shell
  before you can use choco.
Restricting write permissions to Administrators
We are setting up the Chocolatey package repository.
The packages themselves go to 'C:\ProgramData\chocolatey\lib'
  (i.e. C:\ProgramData\chocolatey\lib\yourPackageName).
A shim file for the command line goes to 'C:\ProgramData\chocolatey\bin'
  and points to an executable in 'C:\ProgramData\chocolatey\lib\yourPackageName'.

Creating Chocolatey folders if they do not already exist.

chocolatey.nupkg file not installed in lib.
 Attempting to locate it from bootstrapper.
PATH environment variable does not have C:\ProgramData\chocolatey\bin in it. Adding...
```


설치 완료 후 check
```powershell
> choco
Chocolatey v2.2.2
Please run 'choco -?' or 'choco <command> -?' for help menu.
```

위 같이 되면 설치 완료.

### kind 설치

**kind 란?**
`Kubernetes IN Docker`


```powershell
> choco install kind
chocolatey-dotnetfx.extension v1.0.1 [Approved]
chocolatey-dotnetfx.extension package files install completed. Performing other installation steps.
 Installed/updated chocolatey-dotnetfx extensions.
 The install of chocolatey-dotnetfx.extension was successful.
  Software installed to 'C:\ProgramData\chocolatey\extensions\chocolatey-dotnetfx'
Progress: Downloading KB2919442 1.0.20160915... 100%

KB2919442 v1.0.20160915 [Approved]
KB2919442 package files install completed. Performing other installation steps.
The package KB2919442 wants to run 'ChocolateyInstall.ps1'.
Note: If you don't run this script, the installation will fail.
Note: To confirm automatically next time, use '-y' or consider:
choco feature enable -n allowGlobalConfirmation
Do you want to run the script?([Y]es/[A]ll - yes to all/[N]o/[P]rint): Y

Skipping installation because this hotfix only applies to Windows 8.1 and Windows Server 2012 R2.
 The install of KB2919442 was successful.
  Software install location not explicitly set, it could be in package or
  default install location of installer.
Progress: Downloading KB2919355 1.0.20160915... 100%

KB2919355 v1.0.20160915 [Approved]
KB2919355 package files install completed. Performing other installation steps.
The package KB2919355 wants to run 'ChocolateyInstall.ps1'.
Note: If you don't run this script, the installation will fail.
Note: To confirm automatically next time, use '-y' or consider:
choco feature enable -n allowGlobalConfirmation
Do you want to run the script?([Y]es/[A]ll - yes to all/[N]o/[P]rint): A

Skipping installation because this hotfix only applies to Windows 8.1 and Windows Server 2012 R2.
 The install of KB2919355 was successful.
  Software install location not explicitly set, it could be in package or
  default install location of installer.
Progress: Downloading dotnetfx 4.8.0.20220524... 100%

dotnetfx v4.8.0.20220524 [Approved]
dotnetfx package files install completed. Performing other installation steps.
Microsoft .NET Framework 4.8 or later is already installed.
 The install of dotnetfx was successful.
  Software install location not explicitly set, it could be in package or
  default install location of installer.
Progress: Downloading docker-desktop 4.28.0... 100%

docker-desktop v4.28.0 [Approved]
docker-desktop package files install completed. Performing other installation steps.
Downloading docker-desktop
  from 'https://desktop.docker.com/win/main/amd64/139021/Docker%20Desktop%20Installer.exe'
```

