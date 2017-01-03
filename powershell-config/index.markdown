---
author: sandeep
comments: true
date: 2008-07-11 20:30:08+00:00
layout: default
link: http://www.lambdacurry.com/powershell-config/
slug: powershell-config
title: Powershell Config
wordpress_id: 153
---

[sourcecode lang="powershell"]

# this file is at C:Documents and Settings&lt;username&gt;My DocumentsWindowsPowerShellprofile.ps1

$Host.Ui.RawUi.BackGroundColor = "Black"
cls
set-location d:
$oldPath = get-content Env:Path;
$env:INCLUDE="C:Program FilesMicrosoft Platform SDK for Windows Server 2003 R2Includecrt;"+ "C:Program FilesMicrosoft Platform SDK for Windows Server 2003 R2Include;"
$env:LIB="C:Program FilesMicrosoft Visual Studio 9.0VClib;" +  "C:Program FilesMicrosoft Platform SDK for Windows Server 2003 R2Lib"
$newPath = "C:Program FilesMicrosoft Visual Studio 9.0VCbin;" +$oldPath + ";"+ "C:Program FilesMicrosoft Platform SDK for Windows Server 2003 R2Bin" + ";"+ "C:Program FilesMicrosoft Platform SDK for Windows Server 2003 R2Binwin64" + ";" + "C:Program FilesMicrosoft Visual Studio 9.0Common7ToolsBin" + ";" + ";" +
"C:Program FilesVimvim71";

$env:LS_OPTIONS = "-bhAC --more --color=auto --recent --streams"
set-alias ls "C:WINDOWSsystem32ls.exe" -option allscope
set-content Env:Path $newPath;

[/sourcecode]
