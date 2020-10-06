:local send [:parse [/system script get tg_sendMessage source]]
:local hotspot [:len [/ip hotspot active find]]

:put $params
:put $chatid
:put $from
 
:local text "Router ID:* $[/system identity get name] * %0A\
Uptime: _$[/system resource get uptime]_%0A\
CPU Load: _$[/system resource get cpu-load]%_%0A\
RAM: _$(([/system resource get total-memory]-[/system resource get free-memory])/(1024*1024))M/$([/system resource get total-memory]/(1024*1024))M_"
 
$send chat=$chatid text=$text mode="Markdown"
:return true