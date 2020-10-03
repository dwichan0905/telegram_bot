:local send [:parse [/system script get tg_sendMessage source]]
:put $params
:put $chatid
:put $from

:local text "Force Update DDNS"

$send chat=$chatid text=$text mode="Markdown"
/ip cloud force-update