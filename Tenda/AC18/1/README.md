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
