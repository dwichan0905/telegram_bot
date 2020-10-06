:local send [:parse [/system script get tg_sendMessage source]]

:put $params
:put $chatid
:put $from

:local text "Router ID:* $[/system identity get name] * %0A\
==================%0A\
MENU TERSEDIA%0A\
==================%0A\
/help%0A\
/start%0A\
/cpu%0A\
/interface%0A\
 - show%0A\
/hotspot%0A\
 - session%0A\
   > count%0A\
   > showall%0A\
   > deauth-by-user <username>%0A\
   > deauth-by-mac <mac address>%0A\
   > deauth-by-ip <ip>%0A\
 - add <username> <password>%0A\
 - delete <username>%0A\
 - disable <username>%0A\
 - enable <username>%0A\
 - setprofile <username> <profile>%0A\
 - change-password <username> <password>%0A\
/ping to <ip>%0A\
/public%0A\
/enablehotspot%0A\
/disablehotspot%0A\
/forceupdateddns%0A\
/reboot"
 
$send chat=$chatid text=$text mode="Markdown"
:return true