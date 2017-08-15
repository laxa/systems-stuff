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

## Cortana

To disable Cortana in windows 10

Press Win + R keyboard accelerator to open Run dialog box.
Type GPedit.msc and hit Enter or OK to open Local Group Policy Editor. Navigate to Local Computer Policy -> Computer Configuration -> Administrative Templates -> Windows Components -> Search.
In the right pane, double click on policy named Allow Cortana.
Select the Disabled radio button.
Restart the PC and Cortana and Bing Search will be disabled. (May work after signing out and in again)

source: https://superuser.com/a/951895
