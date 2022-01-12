---
layout: post
title:  "vscode with c++ Windows setup"
date:   2019-04-14 00:00:00 +0800
categories: note
tags: [VScode, C++]
---
## [Download & Install Visual Studio Code](https://code.visualstudio.com)
## [Download & Install MinGW-w64](https://sourceforge.net/projects/mingw-w64/)
Modify "Architecture" in Settings  
![MinGW_1](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/MinGW_1.png?raw=true)  
Modify "Destination folder" in Installation folder  
![MinGW_2](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/MinGW_2.png?raw=true)  
others default is fine  
## [Download & Install LLVM](https://sourceforge.net/projects/mingw-w64/)
Download "Pre-Built Binaries" version  
![LLVM_1](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/LLVM_1.png?raw=true)  
Modify "system PATH" option  
![LLVM_2](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/LLVM_2.png?raw=true)  
Modify "Destination Folder"  
![LLVM_3](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/LLVM_3.png?raw=true)  
## Copy data
Copy data in "C:\mingw-w64\x86_64-8.1.0-posix-seh-rt_v6-rev0\mingw64" to "C:\LLVM"  
![MinGW_LLVM](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/MinGW_LLVM.png?raw=true)  
## Install vscode extensions
![vscode cpp extensions](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/vscode_cpp_extensions.png?raw=true)  
## Create project folder & json file
- Create a project folder, example : "Cpp".
- Create ".vscode" folder in project folder.
- Add 4 json file in .vscode folder :
	- c_cpp_properties.json
```json
{
	"configurations": [
		{
			"name": "MinGW",
			"intelliSenseMode": "clang-x64",
			"compilerPath": "C:/LLVM/bin/gcc.exe",
			"includePath": [
				"${workspaceFolder}"
			],
			"defines": [],
			"browse": {
				"path": [
					"${workspaceFolder}"
				],
				"limitSymbolsToIncludedHeaders": true,
				"databaseFilename": ""
			},
			"cStandard": "c11",
			"cppStandard": "c++17"
		}
	],
	"version": 4
}
```
	- launch.json
```json
{
	"version": "0.2.0",
	"configurations": [
		{
			"name": "(gdb) Launch", 
			"type": "cppdbg", 
			"request": "launch",
			"program": "${fileDirname}/${fileBasenameNoExtension}.exe", 
			"args": [], 
			"stopAtEntry": true,
			"cwd": "${workspaceFolder}",
			"environment": [],
			"externalConsole": true, 
			"internalConsoleOptions": "neverOpen",
			"MIMode": "gdb",
			"miDebuggerPath": "gdb.exe", 
			"setupCommands": [ 
	 			{
					"description": "Enable pretty-printing for gdb",
					"text": "-enable-pretty-printing",
					"ignoreFailures": false
				}
			],
			"preLaunchTask": "Compile" 
		}
	]
}
```
	- settings.json
```json
{
	"files.defaultLanguage": "cpp", 
	"editor.formatOnType": true, 
	"editor.snippetSuggestions": "top",
	"code-runner.runInTerminal": true,
	"code-runner.executorMap": {
		"c": "cd $dir && clang $fileName -o $fileNameWithoutExt.exe -Wall -g -Og -static-libgcc -fcolor-diagnostics --target=x86_64-w64-mingw -std=c11 && $dir$fileNameWithoutExt",
		"cpp": "cd $dir && clang++ $fileName -o $fileNameWithoutExt.exe -Wall -g -Og -static-libgcc -fcolor-diagnostics --target=x86_64-w64-mingw -std=c++17 && $dir$fileNameWithoutExt"
	}, 
	"code-runner.saveFileBeforeRun": true, 
	"code-runner.preserveFocus": true, 
	"code-runner.clearPreviousOutput": false, 
	"C_Cpp.clang_format_sortIncludes": true,
	"C_Cpp.intelliSenseEngine": "Default", 
	"C_Cpp.errorSquiggles": "Disabled", 
	"C_Cpp.autocomplete": "Disabled",
	"clang.cflags": [
		"--target=x86_64-w64-mingw",
		"-std=c11",
		"-Wall"
	],
	"clang.cxxflags": [ 
		"--target=x86_64-w64-mingw",
		"-std=c++17",
		"-Wall"
	],
	"clang.completion.enable": true 
}
```
	- tasks.json
```json
{
	"version": "2.0.0",
	"tasks": [
		{
			"label": "Compile", 
			"command": "clang++", 
			"args": [
				"${file}",
				"-o",
				"${fileDirname}/${fileBasenameNoExtension}.exe",
				"-g", 
				"-Wall",
				"-static-libgcc",
				"-fcolor-diagnostics",
				"--target=x86_64-w64-mingw", 
				"-std=c++17" 
			], 
			"type": "shell", 
			"group": {
				"kind": "build",
				"isDefault": true 
			},
			"presentation": {
				"echo": true,
				"reveal": "always", 
				"focus": false, 
				"panel": "shared" 
			}
		}
	]
}
```  

## Happy coding
- Coding files must be in project folder.
- "Ctrl + Shift + B" to build .exe file.
- "Ctrl + Alt + N" to run.  

![vscode cpp test](https://github.com/nshawn4675/nshawn4675.github.io/blob/master/_pic/vscode_cpp_test.png?raw=true)