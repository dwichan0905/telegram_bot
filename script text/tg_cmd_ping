:local send [:parse [/system script get tg_sendMessage source]]
:local param1 [:pick $params 0 [:find $params " "]]
:local param2 [:pick $params ([:find $params " "]+1) [:len $params]]

:put $params
:put $param1
:put $param2
:put $chatid
:put $from

:if ($param1="to") do={
#Ping Variables
:local avgRtt;
:local pin
:local pout
:local datetime "$[/system clock get date] $[/system clock get time]"
#Ping it real good
/tool flood-ping $param2 count=10 do={
  
:if ($sent = 10) do={
    
:set avgRtt $"avg-rtt"
    
:set pout $sent
    
:set pin $received
  }

}

:local ploss (100 - (($pin * 100) / $pout))

:local logmsg ("Ping Average for $param2 - ".[:tostr $avgRtt]."ms - packet loss: ".[:tostr $ploss]."%")

:log info $logmsg

:local text "Router ID:* $[/system identity get name] * %0A\
Date : _$datetime_%0A\
IP: _$param2_%0A\
Result:%0A_$logmsg_"
$send chat=$chatid text=$text mode="Markdown"
:return true
} else={
#Ping Variables
:local avgRtt;
:local pin
:local pout
:local datetime "$[/system clock get date] $[/system clock get time]"
#Ping it real good
/tool flood-ping 8.8.8.8 count=10 do={
  
:if ($sent = 10) do={
    
:set avgRtt $"avg-rtt"
    
:set pout $sent
    
:set pin $received
  }

}

:local ploss (100 - (($pin * 100) / $pout))

:local logmsg ("Ping Average for 8.8.8.8 - ".[:tostr $avgRtt]."ms - packet loss: ".[:tostr $ploss]."%")

:log info $logmsg

:local text "Router ID:* $[/system identity get name] * %0A\
Date : _$datetime_%0A\
IP: _8.8.8.8_%0A\
Result:%0A_$logmsg_"
$send chat=$chatid text=$text mode="Markdown"
:return true
}