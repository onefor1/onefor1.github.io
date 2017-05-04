入侵的艺术

第一部分：Windows服务器权限分析
一、Windows常见用户 
二、Windows 2003常见组 
三、Windows目录权限 
四、Windows 2003默认权限 
五、不同环境下的木马运行区别
Windows 常见用户 
SYSTEM      本地机器上拥有最高权限的用户 。 
Administrator     基本上是本地机器上拥有最高权限的用户 。 
Guest     只拥有相对极少的权限，在默认情况下是被禁用的 。 

Windows 常见用组 
Administrators     这个用户组在本地机器上拥有最高权限。 
Backup Operators     虽然不如Administrators大，但也差不多。  
Guests     与USER组权限相同。 
Distributed COM Users     分布式系统帐号，涉及到域及域控制器等知识。 
Network Configuration Operators      WINDOWS2003中新增的用户组，这个用户组有足够的权  限去管理网络配置情况。  
Performance Log Users      WINDWOS2003中新增用户组，这个用户有权从远程安排性能计数器的日志工作。 

Windows 常见用组 
Performance Monitor Users     
WINDOWS2003新增用户组，这个用户组有权从远程监控计算机的运行情况。 
Power Users     低于ADMINISTRAOTRS，但远高于GUEST，不能将添加管理员。 
Print Operators     不如ADMINISTRATOR大，但是差不多。   Windows 常见用组 
Users    本地机器上所有的用户帐户：这是一个低权限的用户组。 
IIS_WPG     WINDOWS2003新增用户组：如果安装了IIS，用来运行和种WEB应用程序的帐户将被容纳在这个用户组里。 
Windows 常见用组 

Windows目录权限 
Windows2003 默认权限 默认只安装静态HTTP服务器      
IIS  6.0的默认安装被设置为仅安装静态HTML页面显示所需的组件，而不允许动态内容。  
增强的文件访问控制      
匿名帐号不再具有web服务器根目录的写权限。 

Windows2003 默认权限 父目录被禁用      
IIS6.0中默认禁用了对父目录的访问。这样可以避免攻击者跨越web站点的目录结构，访问服务器上的其他敏感文件，如SAM文件等。 
坚持最小特权原则      IIS  6.0坚持一个基本安全原则--最小特权原则。也就是说，HTTP.sys中所有代码都是以Local  System权限执行的，而所有的工作进程， 都是以Network  Service 的权限执行的。Network Service是Windows 2003中新内置的一个被严格限制的账号。
Windows2003 默认权限 
不同环境下的木马运行区别 
1、直接在系统上面运行木马与Webshell下运行木马区别在哪？ 
答:在系统上运行木马是系统权限运行，在Webshell下运行木马是以当前内置中间件权限运行。  

2、iis、apache与第三方软件搭建的环境，权限区别在哪？ 
答：IIS下是以IIS_IUSER安全帐户运行的，第三软件一般是管理员权限运行的。




