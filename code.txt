@echo off

:: Install Chocolatey (Windows Package Manager) if not installed
powershell -Command "Set-ExecutionPolicy Bypass -Scope Process; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))"

:: Install VS Code
choco install vscode -y

:: Install MinGW (C++ Compiler)
choco install mingw -y

:: Add MinGW to the system PATH
setx PATH "%PATH%;C:\ProgramData\chocolatey\lib\mingw\tools\install\mingw64\bin"

:: Create bits/stdc++.h in MinGW include directory
cd C:\ProgramData\chocolatey\lib\mingw\tools\install\mingw64\include
if not exist bits (
    mkdir bits
)
cd bits
(
echo #ifndef _GLIBCXX_BITS_STDCPP_H
echo #define _GLIBCXX_BITS_STDCPP_H
echo #include <iostream>
echo #include <algorithm>
echo #include <vector>
echo #include <map>
echo #include <set>
echo #include <queue>
echo #include <stack>
echo #include <cmath>
echo #include <cstring>
echo #include <cstdio>
echo #include <cstdlib>
echo #include <climits>
echo #include <utility>
echo #include <numeric>
echo using namespace std;
echo #endif
) > stdc++.h

:: Confirmation message
echo.
echo VS Code, MinGW, and bits/stdc++.h have been successfully installed and configured!
pause
