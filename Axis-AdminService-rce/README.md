# 环境
环境是从官网下载的，如果想要复现，先修改webapps\axis\WEB-INF\web.xml，将以下配置的注释删除，启用axisservlet
<servlet-mapping>
  
    <servlet-name>AxisServlet</servlet-name>
    
    <url-pattern>/servlet/AxisServlet</url-pattern>
    
</servlet-mapping>

如果不是在本地搭环境，还要将server-config.wsdd中的`<parameter name="enableRemoteAdmin" value="false"/> `改为true
# poc链接
写入shell文件到服务器（我是根据这个复现的，此方法不需要之前网上说的Freemarker插件，而Freemarker的jar包默认是没有的）

<https://github.com/KibodWapon/Axis-1.4-RCE-Poc >
# 分析文章
Axis1.4命令执行漏洞<https://bithack.io/forum/376 >

Apache Axis1（<=1.4版本） RCE <https://xz.aliyun.com/t/5513 >
