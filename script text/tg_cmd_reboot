:local send [:parse [/system script get tg_sendMessage source]]
:put $params
:put $chatid
:put $from

:local text "Menghidupkan ulang router dalam 30 detik..."

$send chat=$chatid text=$text mode="Markdown"

:delay 30
system reboot