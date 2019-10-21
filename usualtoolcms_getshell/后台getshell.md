## 说明

此漏洞为后台利用，需要权限。版本：v8

## 漏洞点

/cmsadmin/a_templetex.php中，没有对post穿进的文件名和文件内容，直接利用file_put_contents函数写入文件，所以可直接利用该处漏洞写入shell。
![image](https://github.com/guobaoyou/vul_environment/blob/master/usualtoolcms_getshell/images/code.jpg) 

## 利用

直接构造即可。
![image](https://github.com/guobaoyou/vul_environment/blob/master/usualtoolcms_getshell/images/upload.jpg) 
会在网站目录下生成一个xxxx.php文件，访问时执行phpinfo
![image](https://github.com/guobaoyou/vul_environment/blob/master/usualtoolcms_getshell/images/phpinfo.jpg) 

## 修复

需要判断写入文件的后缀。
