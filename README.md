# aProcessWindows
#include &lt;GuiMenu.au3> #include &lt;WinAPIProc.au3> ; original post at https://www.autoitscript.com/forum/index.php?showtopic=205465&amp;view=findpost&amp;p=1479612 Global $sSCITE_RunAsAdminStr = '/SciteUserIsAdmin:' &amp; IsAdmin() Global $sSCITE_HOME = @ScriptDir &amp; "\SciTE" Global $sSCITE_USERHOME = $sSCITE_HOME &amp; "\SCITE_USERHOME" If IsAdmin() Then $sSCITE_USERHOME = $sSCITE_HOME &amp; "\SCITE_ADMINHOME" Global $sSCITE_EXE = $sSCITE_HOME &amp; "\SciTE.exe" Global $hTimer = TimerInit()  AdlibRegister("OopsyDaisy", 10000) Func OopsyDaisy()     Exit 4 EndFunc  Func GetThisSciteHandle($sSciteUserIsAdmin)     Local $aProcessWindows, $aProcessList = ProcessList("SciTE.exe")     For $n = 1 To UBound($aProcessList) - 1         $aProcessWindows = _WinAPI_EnumProcessWindows($aProcessList[$n][1], 1)         If @error Then ContinueLoop         If StringInStr(_WinAPI_GetProcessCommandLine($aProcessList[$n][1]), $sSciteUserIsAdmin) Then Return $aProcessWindows[1][0]     Next EndFunc   ;==>GetThisSciteHandle
