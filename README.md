# Easy-Windows-Software-Patcher-Batch-Script-
Make a simple windows Patcher using command prompts.
```
@echo off

set ver=v5.3

title EasyPatcher
fltmc >nul 2>&1 || (
  echo Set UAC = CreateObject^("Shell.Application"^) > "%temp%\GetAdmin.vbs"
  echo UAC.ShellExecute "%~fs0", "", "", "runas", 1 >> "%temp%\GetAdmin.vbs"
  cmd /u /c type "%temp%\GetAdmin.vbs">"%temp%\GetAdminUnicode.vbs"
  cscript //nologo "%temp%\GetAdminUnicode.vbs"
  del /f /q "%temp%\GetAdmin.vbs" >nul 2>&1
  del /f /q "%temp%\GetAdminUnicode.vbs" >nul 2>&1
  exit
)

@echo off
SET hosts=%windir%\system32\drivers\etc\hosts
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Cyberlink\PowerDirector19\UserReg" /v "Prod_Activate" /t REG_SZ /d "LocalServer"
attrib -r %hosts%
echo. >>%hosts%
FOR %%A IN (

cap.cyberlink.com
activation.cyberlink.com


) DO (
 echo 127.0.0.1 %%A >>%hosts%
)
attrib +r %hosts%
echo Successfully Patched Internet Access and Registry for Activation
pause


```
