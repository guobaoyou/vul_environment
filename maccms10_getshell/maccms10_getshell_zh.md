
#Maccms 后台任意文件写入致getshell#
##
verison:v10 最新版
官网:http://www.maccms.com/
##

登录后台，点击基础-》分类管理；可以看见每一种类别都是用的分类页模板。并且可以看出该处使用的模板为/art/type.html
![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/1.png)

而在后台可以编辑模板：点击模板-》模板管理，进入到/template/default_pc/html/art的模板管理处，点击编辑
![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/2.png)
输入php代码
![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/3.png)
访问index.php/art/type/id/5.html，PHP代码成功执行。
![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/4.png) 
原理分析：
程序本来设计为禁止将模板改为PHP文件：
![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/7.png)
但是在渲染模板时，程序会将该模板文件写入到缓存文件中，并在之后用include包含，所以在禁止将模板改为php文件后，依旧能执行代码。

 ![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/8.png)
 ![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/6.png)
 ![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/5.png)
  


      
