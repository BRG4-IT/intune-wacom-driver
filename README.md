## Installing Wacom Driver via MS Intune

### Preperation

1. [Download Wacom driver package](https://www.wacom.com/en-en/support/product-support/drivers) (e.g. WacomTablet_6.3.44-3.exe) to your project directory
2. extract package using [7zip](https://www.7-zip.org/download.html) (look for Setup.exe)
3. copy [`Install-Silently.ps1`](./Install-Silently.ps1) to `WacomTablet_6.3.44-3` directory
4. Download the [IntuneWinAppUtil](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool) Programm
5. Move `IntuneWinAppUtil.exe` to the root of this repository
6. Open a command prompt or Powershell console
7. Navigate to your project directory
8. Create an .intunewin file by executing the following command:

```
.\IntuneWinAppUtil.exe -c .\WacomTablet_6.3.44-3 -s Install-Silently.ps1 -o ./
```


## Intune

Add new __Windows app (Win32)__ app.

### Programm

Upload .intunewin file and

Install command (Installationsbefehl):

```
powershell.exe -executionpolicy bypass .\Install-Silently.ps1
```

Uninstall command (Deinstallationsbefehl):

```
powershell.exe -executionpolicy bypass .\Install-Silently.ps1 -uninstall
```

Install behavior (Installationsverhalten): __System__


### Detection Rule

Rule Type (Regeltyp): __Registry__ (__Registrierung__)

Key Path (Schlüsselpfad):

```
HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Wacom Tablet Driver\
```

Value Name (Wertname):

```
DisplayVersion
```

Registry Key Requirement (Erkennungsmethode): __String Comparison (Zeichenfolgenvergleich)__

Operator: __Equals (Ist gleich)__

Value (Wert):

```
6.3.44-3
```

