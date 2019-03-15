#Maccms Background arbitrary file write to getshell#
#CVE-2019-9829#
##
version:v10 
soft download:http://www.maccms.com/
##




Log in to the background, click on Basic -> Category Management; you can see the category page template used for each category. 
And you can see that the template used here is /art/type.html
![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/1.png)

In the background, you can edit the template: Click Template - "Template Management", 
go to the template management area of ./template/default_pc/html/art, click Edit
![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/2.png)
input the php code
![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/3.png)
Visit index.php/art/type/id/5.html and the PHP code executes successfully.
![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/4.png)

##code analysis##:
The program was originally designed to prohibit changing the template to a PHP file:
![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/7.png)
However, when rendering the template, the program will write the template file to the cache file,
and then include it with "include", so after prohibiting the template from being changed to php file, the code can still be executed.

 ![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/8.png)
 ![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/6.png)
 ![image](https://github.com/guobaoyou/vul_environment/blob/master/maccms10_getshell/images/5.png)
