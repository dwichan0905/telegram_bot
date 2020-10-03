:local send [:parse [/system script get tg_sendMessage source]]
:local param1 [:pick $params 0 [:find $params " "]]
:local param2 [:pick $params ([:find $params " "]+1) [:len $params]]
:local param3 [:pick [:pick $params ([:find $params " "]+1) [:len $params]] ([:find [:pick $params ([:find $params " "]+1) [:len $params]] " "]+1) [:len [:pick $params ([:find $params " "]+1) [:len $params]]]]
:if ([:len [:find $param2 " "]]>0) do={
	:set param2 [:pick [:pick $params ([:find $params " "]+1) [:len $params]] 0 [:find [:pick $params ([:find $params " "]+1) [:len $params]] " "]]
} else={
	:set param3 ""
}

:put $params
:put $param1
:put $param2
:put $param3
:put $chatid
:put $from

:if ($param1="session") do={
:if ($param2="count") do={
:local output
:local hotspot [:len [/ip hotspot active find]]
:local text "Router ID:* $[/system identity get name] * %0A\
Hotspot users: _$hotspot online_"

$send chat=$chatid text=$text mode="Markdown"
}
:if ($param2="showall") do={
:local output
:foreach activeIndex in=[/ip hotspot active find] do={
:local activeUser ("*Username*: ".[/ip hotspot active get value-name="user" $activeIndex]."%0A")
:local activeAddress ("*IP*: ".[/ip hotspot active get value-name="address" $activeIndex]."%0A")
:local activeMACAddr ("*MAC*: ".[/ip hotspot active get value-name="mac-address" $activeIndex]."%0A")
:local activeLoginBy ("*Login Method*: ".[/ip hotspot active get value-name="login-by" $activeIndex]."%0A")
:local activeUptime ("*Uptime*: ".[/ip hotspot active get value-name="uptime" $activeIndex]."%0A")
:local idletime ("*Idle Time*: ".[/ip hotspot active get value-name="idle-time" $activeIndex]."%0A")
:local serverIn ("*Server*: ".[/ip hotspot active get value-name="server" $activeIndex]."%0A")
:set output ($output.$activeUser.$activeAddress.$activeMACAddr.$activeUptime.$idletime.$activeLoginBy.$serverIn."%0A")
}
$send chat=$chatid text=("$output") mode="Markdown"
}
:if ($param2="deauth-by-user") do={
/ip hotspot active remove [find user="$param3"]
$send chat=$chatid text=("Sesi User $param3 berhasil dihapus") mode="Markdown"
}
:if ($param2="deauth-by-mac") do={
/ip hotspot active remove [find mac-address="$param3"]
$send chat=$chatid text=("Sesi MAC $param3 berhasil dihapus") mode="Markdown"
}
:if ($param2="deauth-by-ip") do={
/ip hotspot active remove [find address="$param3"]
$send chat=$chatid text=("Sesi IP $param3 berhasil dihapus") mode="Markdown"
}
}
:if ($param1="add") do={
/ip hotspot user add name=$param2 password=$param3 profile=default
$send chat=$chatid text=("Berhasil membuat user baru. Masuk ke hotspot dengan:%0A%0A*Username:* $param2%0A*Password:* $param3") mode="Markdown"
}
:if ($param1="delete") do={
/ip hotspot user remove [find name=$param2]
$send chat=$chatid text=("Berhasil menghapus user $param2.") mode="Markdown"
}
:if ($param1="disable") do={
/ip hotspot user disable [find name=$param2]
$send chat=$chatid text=("$param2 kini telah dinonaktifkan") mode="Markdown"
}
:if ($param1="enable") do={
/ip hotspot user enable [find name=$param2]
$send chat=$chatid text=("$param2 kini telah diaktifkan") mode="Markdown"
}
:if ($param1="setprofile") do={
/ip hotspot user set password=$param3 [find name=$param2]
/ip hotspot active remove [find name=$param2]
$send chat=$chatid text=("Berhasil mengganti profile menjadi $param3.") mode="Markdown"
}
:if ($param1="change-password") do={
/ip hotspot user set password=$param3 [find name=$param2]
/ip hotspot active remove [find name=$param2]
$send chat=$chatid text=("Berhasil mengganti password untuk $param2.") mode="Markdown"
}
$send chat=$chatid text=("$output") mode="Markdown"
}