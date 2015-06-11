#
    Open Notepad
    Copy the following text and paste it into Notepad:

REG QUERY "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\UpgradeExperienceIndicators" /v UpgEx | findstr UpgEx

if "%errorlevel%" == "0" GOTO RunGWX

reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Appraiser" /v UtcOnetimeSend /t REG_DWORD /d 1 /f

schtasks /run /TN "\Microsoft\Windows\Application Experience\Microsoft Compatibility Appraiser"

:CompatCheckRunning

schtasks /query /TN "\Microsoft\Windows\Application Experience\Microsoft Compatibility Appraiser"

schtasks /query /TN "\Microsoft\Windows\Application Experience\Microsoft Compatibility Appraiser" | findstr Ready

if NOT "%errorlevel%" == "0" ping localhost >nul &goto :CompatCheckRunning

:RunGWX

schtasks /run /TN "\Microsoft\Windows\Setup\gwx\refreshgwxconfig"


    Click File, and then Save As

    In the File name box, change the file name to ReserveWin10.cmd

    Then click the dropdown next to Save as type, and select All files (*.*)

    Select the folder you would like to save the file to.  For this example, let’s choose to save the file to the C:/Temp folder.  Then click Save. 

    Open an elevated command prompt.  (From the Start screen or Start menu, type Command Prompt in the search box, and then in the list of results, right-click Command Prompt, and select Run as administrator.)

    Finally, run the file from the location you saved to in Step 6.  In this example, you would type the following in the Command Prompt window and hit Enter:

    C:/Temp/ReserveWin10.cmd
