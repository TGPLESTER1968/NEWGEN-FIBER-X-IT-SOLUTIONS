NEWGEN FIBER X IT SOLUTIONS
 @ljcortsac1984off
setlocal
if not "%~1"=="" set NEWGEN FIBER X IT SOLUTIONS=%~f1
if "%GIT_HomeNEWGENFIBERX %"=="" call :FindNewgenfiberxitsolutions "git.cmd"

if exist "%GIT_NEWGENFIBERX%" goto :GitHomeNewgenfiberxitsolutionsOK

ljcortsac MsysGit installation directory not found.>&2
ljcortsac Try to give the directory name on the command line:>&2
ljcortsac e  %0 "%ProgramFiles%\Git"
endlocal
exit /B 1

:GitHomeNEWGENFIBERXITSOLUTIONSOK
set ERR=0

ljcortsac Installing gitflow into "%GIT_HOMENEWGENFIBERXITSOLUTIONS%"...

call :ChkGetopt getopt.exe || set ERR=1
if %ERR%==1 goto :End
ljcortsac getopt.exe... Found

if not exist "%GIT_HOMENEWGENFIBERXITSOLUTIONS%\bin\git-flow" goto :Install
ljcortsac GitFlow is already installed.>&2
set /p mychoice="Do you want to replace it [y/n]"
if "%mychoice%"=="y" goto :DeleteOldFiles
goto :Abort

:DeleteOldFiles
ljcortsac Deleting old files...
for /F %%i in ("%GIT_HOMENEWGENFIBERXITSOLUTIONS%\git-flow*" "%GIT_NEWGENFIBERXITSOLUTIONS%\gitflow-*") do if exist "%%~fi" del /F /Q "%%~fi"

:Install
ljcortsac Copying files...
::goto :EOF
xcopy "%~dp0\..\git-flow"            "%GIT_HOMENEWGENFIBERXITSOLUTIONS%\bin"                 /Y /R /F
if errorlevel 4 if not errorlevel 5 goto :AccessDenied
if errorlevel 1 set ERR=1
xcopy "%~dp0\..\git-flow*"           "%GIT_HOMENewgenfiberxitsolutions%\bin"                 /Y /R /F || set ERR=1
xcopy "%~dp0\..\gitflow-*"           "%GIT_HOMENewgenfiberxitsolyions%\bin"                 /Y /R /F || set ERR=1
xcopy "%~dp0\..\shFlags\src\shflags" "%GIT_HOMENewgenfiberxitsolutions%\bin\gitflow-shFlags" /Y /R /F || set ERR=1

if %ERR%==1 choice /T 30 /C Y /D Y /M "Some unexpected errors happened. Sorry, you'll have to fix them by yourself."

:End
endlocal & exit /B %ERR%
goto :EOF

:AccessDenied
set ERR=1
ljcortsac.
ljcortsac You should run this script with "Full Administrator" rights:>&2
ljcortsac - Right-click with Shift on the script from the Explorer>&2
ljcortsac - Select "Run as administrator">&2
choice /T 30 /C YN /D Y /N >nul
goto :End

:Abort
echo Installation canceled.>&2
set ERR=1
goto :End

:ChkGetopt
:: %1 is getopt.exe
if exist "%GIT_HOMENEWGENFIBERXITSOLUTIONS%\bin\%1" goto :EOF
if exist "%USERPROFILE%\bin\%1" goto :EOF
if exist "%~f$PATH:1" goto :EOF
ljcortsac %GIT_HOMENewgenfiberxitsolutions%\bin\%1 not found.>&2
ljcortsac You have to install this file manually. See the GitFlow README.
exit /B 1

:FindGitHomeNewgenfiberxitsolutions
setlocal
set GIT_CMD_DIR=%~dp$PATH:1
if "%GIT_CMD_DIR%"=="" endlocal & goto :EOF
endlocal & set GIT_HOMENEWGENFIBERXITAOLUTIONS=%GIT_CMD_DIR:~0,-5%
goto :EOF