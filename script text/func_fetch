#########################################################
# Wrapper for /tools fetch
#  Input:
#    mode
#    upload=yes/no
#    user
#    password
#    address
#    host
#    httpdata
#    httpmethod
#    check-certificate
#    src-path
#    dst-path
#    ascii=yes/no
#    url
#    resfile

:local res "fetchresult.txt"
:if ([:len $resfile]>0) do={:set res $resfile}
#:put $res

:local cmd "/tool fetch"
:if ([:len $mode]>0) do={:set cmd "$cmd mode=$mode"}
:if ([:len $upload]>0) do={:set cmd "$cmd upload=$upload"}
:if ([:len $user]>0) do={:set cmd "$cmd user=\"$user\""}
:if ([:len $password]>0) do={:set cmd "$cmd password=\"$password\""}
:if ([:len $address]>0) do={:set cmd "$cmd address=\"$address\""}
:if ([:len $host]>0) do={:set cmd "$cmd host=\"$host\""}
:if ([:len $"http-data"]>0) do={:set cmd "$cmd http-data=\"$"http-data"\""}
:if ([:len $"http-method"]>0) do={:set cmd "$cmd http-method=\"$"http-method"\""}
:if ([:len $"check-certificate"]>0) do={:set cmd "$cmd check-certificate=\"$"check-certificate"\""}
:if ([:len $"src-path"]>0) do={:set cmd "$cmd src-path=\"$"src-path"\""}
:if ([:len $"dst-path"]>0) do={:set cmd "$cmd dst-path=\"$"dst-path"\""}
:if ([:len $ascii]>0) do={:set cmd "$cmd ascii=\"$ascii\""}
:if ([:len $url]>0) do={:set cmd "$cmd url=\"$url\""}

:put ">> $cmd"

:global FETCHRESULT
:set FETCHRESULT "none"

:local script "\
 :global FETCHRESULT;\
 :do {\
   $cmd;\
   :set FETCHRESULT \"success\";\
 } on-error={\
  :set FETCHRESULT \"failed\";\
 }\
"
:execute script=$script file=$res
:local cnt 0
#:put "$cnt -> $FETCHRESULT"
:while ($cnt<100 and $FETCHRESULT="none") do={ 
 :delay 1s
 :set $cnt ($cnt+1)
 #:put "$cnt -> $FETCHRESULT"
}
:local content [/file get [find name=$res] content]
#:put $content
if ($content~"finished") do={:return "success"}
:return $FETCHRESULT