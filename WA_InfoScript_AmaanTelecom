 #### AMAAN TELECOM ####
#خدمة التنبيهات لحالة الروتر
#برمجة فريق أمان تيليكوم للخدمات التقنية
#المهندس/ جنيد باوزير 733996612
#المهندس/ منير الشريف 777638900
#www.facebook.com/AmaanTelcom
#######################
:global apikey;
:global phone;

:do {
:log warning "START Sending to whatsapp";
:local TIME [/system clock get time];
:local ID "$([/system routerboard get model])+$([/system identity get name])";
:local UPTIME [/system resource get uptime];
:local CPU [/system resource get cpu-load];
:local ACTIVE [:len [/ip hotspot active find]];
:local HOST [:len [/ip hotspot host find]];
:local SPEED "";
:do {
:foreach i in=([ /interface find where type=ether or type=bridge or type=vlan and running=yes ]) do={
:local iname ([ /interface get $i name; ]);
#:put $iname;
:local RX (([/interface monitor-traffic $iname as-value once]->"rx-bits-per-second")/1024);
:local TX (([/interface monitor-traffic $iname as-value once]->"tx-bits-per-second")/1024);
:local DATA ((([/interface get $iname rx-byte]+[/interface get $iname tx-byte])/1024)/1024);
:set SPEED ( $SPEED . ("_$iname:_+$RX+%E2%81%84+$TX+%E2%96%BA+$DATA+mb%0A") );
#:log warning "$SPEED";
}
#:log warning "$SPEED";
#:put "$SPEED";
  } on-error={:log warning message=("error getting WAN interface for whatsapp service")}

:local url "https://api.callmebot.com/whatsapp.php?phone=$phone&text=*(%20%D9%85%D8%B9%D9%84%D9%88%D9%85%D8%A7%D8%AA%20%D8%A7%D9%84%D8%AA%D8%B4%D8%BA%D9%8A%D9%84%20)%20%D8%A3%D9%85%D8%A7%D9%86%20%D8%AA%D9%8A%D9%84%D9%8A%D9%83%D9%88%D9%85:*+%0A*%D8%A7%D9%84%D9%88%D9%82%D8%AA:*+$TIME%0A*%D8%A7%D9%84%D8%B1%D9%88%D8%AA%D8%B1:*+$ID%0A*%D9%88%D9%82%D8%AA%20%D8%A7%D9%84%D8%AA%D8%B4%D8%BA%D9%8A%D9%84:*+$UPTIME%0A*%D8%A7%D9%84%D9%85%D8%B9%D8%A7%D9%84%D8%AC:*+$CPU%0A*%D8%A7%D9%84%D8%A7%D9%83%D8%AA%D9%81:*+$ACTIVE%0A*%D8%A7%D9%84%D9%87%D9%88%D8%B3%D8%AA:*+$HOST%0A*%D8%A7%D9%84%D8%B3%D8%B1%D8%B9%D8%A9%20%D9%88%D8%A5%D8%B3%D8%AA%D9%87%D9%84%D8%A7%D9%83%20%D8%A7%D9%84%D8%A8%D9%8A%D8%A7%D9%86%D8%AA:*%0A+$SPEED&apikey=$apikey";
:log info $url;
/tool fetch url=$url dst-path=wp_response.txt;
:delay 2;
:local result [/file get wp_response.txt contents];
:local resultLen [ :len $result ] ;
:log warning ("Finish: " . [:pick $result  ($resultLen-37) $resultLen ]);
:set result ( $result . ("\n$url") );
#:log warning "result $result";
  } on-error={:log error message=("error")}
 }
 
