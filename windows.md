# Windows

## UAC hardening

`Control Panel` => `Change User Account Control settings` => Set to `Always notify`

windows+r shortcut => `gpedit.msc` => browse `Computer Configuration/Windows Settings/Securiry Settings/Local Policies/Security Options`
Then set `User Account Control: Behavior of the elevation prompt for administrators in Admin Approval Mode` to `Prompt for credentials`
Then set `User Account Control: Behavior of the elevation prompt for standard users` to `Prompt for credentials`

https://www.sevenforums.com/tutorials/77389-uac-require-password-administrator.html
https://superuser.com/questions/1085680/windows-10-make-uac-always-require-password

## Crash reports

Disabling crash reports: https://www.lifewire.com/how-do-i-disable-error-reporting-in-windows-2626074

## Services to disable

Access services with windows + r => `services.msc`:
* WebClient
* SSH Server Proxy
* SSH Server Broker

## Cortana

To disable Cortana in windows 10

Press Win + R keyboard accelerator to open Run dialog box.
Type GPedit.msc and hit Enter or OK to open Local Group Policy Editor. Navigate to Local Computer Policy -> Computer Configuration -> Administrative Templates -> Windows Components -> Search.
In the right pane, double click on policy named Allow Cortana.
Select the Disabled radio button.
Restart the PC and Cortana and Bing Search will be disabled. (May work after signing out and in again)

source: https://superuser.com/a/951895

## Windows cached logons

Login through networks can be cached by the system allowing users on the machine to potentially retrieve hash/creds on the machine, to check this settings, run:
```
REG QUERY "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v CachedLogonsCount
```

This value is set to 10 by default and you should be set to 0 for maximum security.

## Disabling autorun

The following keys have to be set to those values to disable autoplay/autorun on Windows:
`HK(LM|CU)\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer`:
`NoDriveTypeAutoRun` to `0xb5`
`NoDriveAutoRun` to `0x3FFFFFF`

[Documentation](https://technet.microsoft.com/en-us/library/cc938275.aspx)

## Enable sandbox for Windows defender

```
setx /M MP_FORCE_USE_SANDBOX 1
```
And then restart the machine.

[Documentation](https://cloudblogs.microsoft.com/microsoftsecure/2018/10/26/windows-defender-antivirus-can-now-run-in-a-sandbox/)
