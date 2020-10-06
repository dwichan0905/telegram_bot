:local send [:parse [/system script get tg_sendMessage source]]
:put $params
:put $chatid
:put $from

:local reportBody ""
 
:local deviceName [/system identity get name]
:local deviceDate [/system clock get date]
:local deviceTime [/system clock get time]
:local hwModel [/system routerboard get model]
:local rosVersion [/system package get system version]
:local currentFirmware [/system routerboard get current-firmware]
:local upgradeFirmware [/system routerboard get upgrade-firmware]
 
 
:set reportBody ($reportBody . "Router Reboot Report for $deviceName%0A")
:set reportBody ($reportBody . "Report generated on $deviceDate at $deviceTime%0A%0A")
 
:set reportBody ($reportBody . "Hardware Model: $hwModel%0A")
:set reportBody ($reportBody . "RouterOS Version: $rosVersion%0A")
:set reportBody ($reportBody . "Current Firmware: $currentFirmware%0A")
:set reportBody ($reportBody . "Upgrade Firmware: $upgradeFirmware")
if ( $currentFirmware < $upgradeFirmware) do={
:set reportBody ($reportBody . "NOTE: You should upgrade the RouterBOARD firmware!%0A")
}
 
:set reportBody ($reportBody . "%0A%0A=== Critical Log Events ===%0A" )
 
:local x
:local ts
:local msg
foreach i in=([/log find where topics~"critical"]) do={
:set $ts [/log get $i time]
:set $msg [/log get $i message]
:set $reportBody ($reportBody  . $ts . " " . $msg . "%0A" )
}
 
:set reportBody ($reportBody . "%0A=== end of report ===%0A")
$send chat=$chatid text=$reportBody mode="Markdown"