:local send [:parse [/system script get tg_sendMessage source]]
:put $params
:put $chatid
:put $from

:local text "All hotspots disabled"

$send chat=$chatid text=$text mode="Markdown"
/ip hotspot disable lantai1
/ip hotspot disable lantai2