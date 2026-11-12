# VBS

Set objShell = CreateObject("WScript.Shell")
Set objFSO = CreateObject("Scripting.FileSystemObject")

Dim wifiName
wifiName = "TP-Link_526"
Dim notepadFileName
notepadFileName = "pass.txt"

Set x = CreateObject("WScript.Shell")

x.SendKeys "^{ESC}"
WScript.Sleep(1000)

x.SendKeys "cmd"
WScript.Sleep(500)
x.SendKeys "{ENTER}"
WScript.Sleep(2000)

x.SendKeys "netsh wlan show profiles """ & wifiName & """ key=clear | clip"
WScript.Sleep(100)
x.SendKeys "{ENTER}"
WScript.Sleep(100)

x.SendKeys "exit"
WScript.Sleep(100)
x.SendKeys "{ENTER}"
WScript.Sleep(100)

strScriptDir = objFSO.GetParentFolderName(WScript.ScriptFullName)

strFilePath = objFSO.BuildPath(strScriptDir, notepadFileName)

If objFSO.FileExists(strFilePath) Then
    ' Open Notepad with the specified file
    objShell.Run "notepad.exe " & strFilePath
Else
    WScript.Echo "File not found: " & strFilePath
End If
