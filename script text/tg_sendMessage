:local fconfig [:parse [/system script get tg_config source]]

:local cfg [$fconfig]
:local chatID ($cfg->"defaultChatID")
:local botID ($cfg->"botAPI")
:local storage ($cfg->"storage")

:if ([:len $chat]>0) do={:set chatID $chat}

:local url "https://api.telegram.org/bot$botID/sendmessage?chat_id=$chatID&text=$text"
:if ([:len $mode]>0) do={:set url ($url."&parse_mode=$mode")}

:local file ($tgStorage."tg_get_updates.txt")
:local logfile ($tgStorage."tg_fetch_log.txt")

/tool fetch url=$url keep-result=no