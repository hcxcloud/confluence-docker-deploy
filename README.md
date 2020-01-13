# 系统环境
**系统: CentOS 7.6**

**SElinux: Disabled**

**Firewalld： stop**

# Docker 安装
```bash
curl -o /etc/yum.repos.d/docker-ce.repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
yum install -y docker-ce-18.09.9-3.el7
mkdir -p /etc/docker/
cat > /etc/docker/daemon.json << 'EOF'
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
EOF
systemctl enable docker
systemctl start docker
```

# Docker Compose 安装
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
docker-compose --version
```



# Confluence 部署
Git 安装
```bash
yum install -y git
```
下载
```bash
cd /opt
git clone https://github.com/hcxcloud/confluence-docker-deploy.git
```
一键安装
> 如果内存不够可以试着修改 docker-compose.yaml，不懂就自己百度百度

```bash
cd /opt/confluence-docker-deploy/
docker-compose up -d
```

浏览器输入你的主机 ip:8090 进入 Web 界面

**破解**
- -m: 邮箱
- -n: 许可证名字
- -p: 破解的项目名--conf
- -o: 许可组织，填写你的 http 请求地址即可
- -s: 服务器 ID

```bash
docker exec confluence bash -c "java -jar /opt/atlassian-agent.jar -m test@test.com -n test -p conf -o http://192.168.1.100:8090/ -s BQ1E-VJE3-GM70-3NM0"
```

将输出的许可证粘贴至 Web 界面即可

Next 到数据库配置界面

数据库连接配置填写如下:
- 数据库类型: MySQL
- 主机: database
- 端口: 3306
- 数据库: confluence
- 用户名: confluence
- 密码: confluence@123



最后

感谢大神的破解 [https://gitee.com/pengzhile/atlassian-agent](https://gitee.com/pengzhile/atlassian-agent)
