:local send [:parse [/system script get tg_sendMessage source]]
:put $params
:put $chatid
:put $from

:local text "All hotspots enabled"

$send chat=$chatid text=$text mode="Markdown"
/ip hotspot enable lantai1
/ip hotspot enable lantai2