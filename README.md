# DisplayRefreshSetter


winget install --accept-source-agreements --accept-package-agreements --exact --id "Microsoft.VisualStudio.2022.BuildTools" --override "--quiet --wait --norestart --add Microsoft.VisualStudio.Component.VC.Tools.x86.x64 --add Microsoft.VisualStudio.Component.Windows11SDK.26100"





🔧 Изменить Build Tools
 1. Найди Visual Studio Build Tools
 2. Нажми Modify
 3. В разделе Workloads:
 • ☑ C++ build tools
 4. В Individual components проверь:
 • ☑ MSVC v143 - VS 2022 C++ x64/x86 build tools
 • ☑ Windows 10 SDK или Windows 11 SDK
 5. Нажми Modify / Install
 6. Дождись окончания
 7. Перезагрузи систему (желательно)



& "C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\VC\Auxiliary\Build\vcvars64.bat"

rc src\app.rc
cl /nologo ^
   /std:c++17 ^
   /O2 /GL ^
   /DNDEBUG ^
   /MT ^
   /W4 ^
   /EHsc ^
   src\DisplayRefreshRateSetter.cpp src\app.res ^
   /link ^
   /LTCG ^
   /INCREMENTAL:NO ^
   /SUBSYSTEM:CONSOLE ^
   /OPT:REF /OPT:ICF




**DisplayRefreshSetter** is a small native Win32 utility for Windows 10–11 that allows you to set custom refresh rates for specific displays from the command line.

It supports safe mode switching with a confirmation dialog (similar to the system behavior) and an optional `--force` flag for immediate application without rollback.

---

## Features

- Set refresh rate per display (`DISPLAY1`, `DISPLAY2`)
- Native C++ WinAPI (no .NET, no PowerShell, no dependencies)
- System-like confirmation dialog with automatic rollback
- 5-minute timeout before reverting changes
- Optional `--force` mode to skip confirmation
- Works on Windows 10 and Windows 11

---

## Usage

### Basic usage

```powershell
DisplayRefreshSetter.exe --D1=240 --D2=144

This will:
	•	Set DISPLAY1 to 240 Hz
	•	Set DISPLAY2 to 144 Hz
	•	Show a confirmation window
	•	Automatically revert changes after 5 seconds if not confirmed

⸻

Force mode (no confirmation)

DisplayRefreshSetter.exe --D1=240 --force

This will:
	•	Apply the refresh rate immediately
	•	Skip the confirmation dialog
	•	Keep the changes permanently

⚠️ Warning:
Use --force only if you are confident the selected refresh rate is supported by your monitor

⸻

Build Instructions

Requirements
	•	Windows 10 or Windows 11
	•	Microsoft Visual Studio (MSVC)
	•	Win32 Desktop Development tools

Build from Developer Command Prompt

cl /EHsc /W4 /DUNICODE /D_UNICODE DisplayRefreshSetter.cpp user32.lib 

The resulting executable will be:

DisplayRefreshSetter.exe

⸻

Disclaimer

Incorrect refresh rate settings may result in:
	•	Temporary black screen
	•	Unsupported display mode
	•	Automatic rollback by Windows

Always verify your monitor capabilities before using --force.

---




