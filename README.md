README - Final Version?
=======================

Windows Setup
-------------

### Debloat Windows

Run the debloat win 11 scripts.

See the [Github project](https://github.com/Raphire/Win11Debloat) for more details.

```powershell
# Run the script to run the default settings
& ([scriptblock]::Create((irm "https://win11debloat.raphi.re/"))) -RunDefaults -Silent
```

```powershell
# Run this to use my personal settings
& ([scriptblock]::Create((irm "https://win11debloat.raphi.re/"))) -RunDefaults -Silent -ClearStart -ClearStartAllUsers -DisableTelemetry -DisableSuggestions	-DisableLockscreenTips -RevertContextMenu -ShowHiddenFolders -ShowKnownFileExt -TaskbarAlignLeft -HideSearchTb -HideTaskview -HideChat -DisableWidgets -DisableCopilot -DisableRecall -HideGallery -HideHome -ExplorerToHome -HideOnedrive -Hide3dObjects -HideMusic -HideIncludeInLibrary -HideGiveAccessTo -HideShare
```

### WinGet

win_get works great for installing programs these days. Update WinGet settings if required. `telemetry` and `portablePackageUserRoot` may be useful.

[WinGet settings documentation](https://learn.microsoft.com/en-us/windows/package-manager/winget/settings)

```shell
winget settings
```

#### Example of my win_get `settings.json`
```jsonc
{
    // For documentation on these settings, see: https://aka.ms/winget-settings
    "$schema": "https://aka.ms/winget-settings.schema.json",
    "source": {
       "autoUpdateIntervalInMinutes": 120
    },
    "visual": {
        "anonymizeDisplayedPaths": true,
        "enableSixels": true,
        "progressBar": "rainbow"
    },
    "installBehavior": {
        // Defaults to %LOCALAPPDATA%/Microsoft/WinGet/Packages/
        "portablePackageUserRoot": "C:/Users/Dev/Desktop/Portable Apps",
        // Defaults to %PROGRAMFILES%/WinGet/Packages/
        "portablePackageMachineRoot": "C:/Program Files/Packages/Portable",
        "preferences": {
            "architectures": ["x64"],
            // "scope": "user"
        }
    },
    "telemetry": {
        "disable": true
    }
}
```


### Install Programs from WinGet

You can search using `winget serach <package>`.

Alternatively, you can browse this site [winget.run](https://winget.run/) or [winstall.app](https://winstall.app/apps).

#### Replace Windows default programs

```shell
# Install Windows Photos app altnerative
winget install -e --id=DuongDieuPhap.ImageGlass

# Install Media Player alternative
winget install -e --id=clsid2.mpc-hc  # Media Player Classic
# OR
winget install -e --id=VideoLAN.VLC   # VLC

# Install Edge browser alternative
winget install -e --id=eloston.ungoogled-chromium  # Un-googled Chromium
# OR
winget install -e --id=Hibbiki.Chromium  # Chromium Stable builds
```


#### Install other programs as required.

```shell
winget install -e --id=KeePassXCTeam.KeePassXC
winget install -e --id=Git.Git
winget install -e --id=Postman.Postman
# Hack Nerd Fonts
winget install -e --id=SourceFoundry.HackFonts
winget install -e --id=7zip.7zip
winget install -e --id=Mozilla.Firefox
winget install -e --id=Jellyfin.Server
# Motrix Download Manager
winget install -e --id=agalwood.Motrix
winget install -e --id=NordSecurity.NordVPN
winget install -e --id=nzbget.nzbget
winget install -e --id=PicoTorrent.PicoTorrent
winget install -e --id=Rufus.Rufus
winget install -e --id=Win32diskimager.win32diskimager
# FTP SFTP client
winget install -e --id=WinSCP.WinSCP

# TODO

# Docker Desktop
winget install -e --id=Docker.DockerDesktop

# M$
winget install -e --id=Microsoft.WindowsTerminal.Preview
winget install -e --id=Microsoft.VisualStudioCode

```

### Python 3 (Windows)

Install Python 3.13.

```shell
winget install --exact --id Python.Python.3.13 --custom "PrependPath=1 Include_doc=0"
```

### Chocolatey Package Manager

Install Chocolatey (choco) - this is optional.

`win_get` is great for program installs and all, but `choco` can be better suited for libraries, fonts, etc. 

#### choco setup
```shell
Start-Process powershell -Verb runAs  # Start powershell as admin
Set-ExecutionPolicy Bypass -Scope Process -Force
iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

# Re-launch shell and check version
choco --version

# Optional- Disable prompt allowing for automated installs
#   https://docs.chocolatey.org/en-us/configuration/#allowglobalconfirmation
choco feature enable -n allowGlobalConfirmation
```

#### choco package installs
```shell
# Install Hack fonts is not already done
choco install nerd-fonts-hack

# Tailblazer
choco install tailblazer

# TODO
```

### Disable Bluetooth

Bluetooth can be disabled with the following commands:

```powershell
Start-Process powershell -Verb runAs
netsh interface set interface name="Bluetooth Network Connection" admin=disabled
```

```shell
SC config bthserv start= auto
SC config bthHFSrv start= auto 
```
