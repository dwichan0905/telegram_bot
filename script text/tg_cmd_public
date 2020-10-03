:local send [:parse [/system script get tg_sendMessage source]]
:put $params
:put $chatid
:put $from

:local public;

:local ddns;

:set public [/ip cloud get public-address];

:set ddns [/ip cloud get dns-name];

:local text "DDNS : $ddns : IP Public : $public"


$send chat=$chatid text=$text mode="Markdown"