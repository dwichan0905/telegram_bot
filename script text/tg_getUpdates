:global TGLASTMSGID
:global TGLASTUPDID

:local fconfig [:parse [/system script get tg_config source]]
:local http [:parse [/system script get func_fetch source]]
:local gkey [:parse [/system script get tg_getkey source]]
:local send [:parse [/system script get tg_sendMessage source]]

:local cfg [$fconfig]
:local trusted [:toarray ($cfg->"trusted")]
:local botID ($cfg->"botAPI")
:local storage ($cfg->"storage")
:local timeout ($cfg->"timeout")

:put "cfg=$cfg"
:put "trusted=$trusted"
:put "botID=$botID"
:put "storage=$storage"
:put "timeout=$timeout"

:local file ($storage."tg_get_updates.txt")
:local logfile ($storage."tg_fetch_log.txt")
#get 1 message per time
:local url ("https://api.telegram.org/bot".$botID."/getUpdates?timeout=$timeout&limit=1")
:if ([:len $TGLASTUPDID]>0) do={
  :set url "$url&offset=$($TGLASTUPDID+1)"
}

:put "Reading updates..."
:local res [$http dst-path=$file url=$url resfile=$logfile]
:if ($res!="success") do={
  :put "Error getting updates"
  return "Failed get updates"
}
:put "Finished to read updates."

:local content [/file get [/file find name=$file] contents]

:local msgid [$gkey key="message_id" text=$content]
:if ($msgid="") do={ 
 :put "No new updates"
 :return 0 
}
:set TGLASTMSGID $msgid

:local updid [$gkey key="update_id" text=$content]
:set TGLASTUPDID $updid

:local fromid [$gkey block="from" key="id" text=$content]
:local username [$gkey block="from" key="username" text=$content]
:local firstname [$gkey block="from" key="first_name" text=$content]
:local lastname [$gkey block="from" key="last_name" text=$content]
:local chatid [$gkey block="chat" key="id" text=$content]
:local chattext [$gkey block="chat" key="text" text=$content]

:put "message id=$msgid"
:put "update id=$updid"
:put "from id=$fromid"
:put "first name=$firstname"
:put "last name=$lastname"
:put "username=$username"
:local name "$firstname $lastname"
:if ([:len $name]<2) do {
 :set name $username
}

:put "in chat=$chatid"
:put "command=$chattext"

:local allowed ( [:type [:find $trusted $fromid]]!="nil" or [:type [:find $trusted $chatid]]!="nil")
:if (!$allowed) do={
 :put "Unknown sender, keep silence"
 :return -1
}

:local cmd ""
:local params ""
:local ltext [:len $chattext]

:local pos [:find $chattext " "]
:if ([:type $pos]="nil") do={
 :set cmd [:pick $chattext 1 $ltext]
} else={
 :set cmd [:pick $chattext 1 $pos]
 :set params [:pick $chattext ($pos+1) $ltext]
}

:local pos [:find $cmd "@"]
:if ([:type $pos]!="nil") do={
 :set cmd [:pick $cmd 0 $pos]
}

:put "cmd=<$cmd>"
:put "params=<$params>"

:global TGLASTCMD $cmd

:put "Try to invoke external script tg_cmd_$cmd"
:local script [:parse [/system script get "tg_cmd_$cmd" source]]
$script params=$params chatid=$chatid from=$name