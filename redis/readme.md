## 安装
[安装参考](https://zhuanlan.zhihu.com/p/626263224)
```
# 安装
yum install redis

# 查看版本信息
redis-server -v

# 启动
systemctl start redis


# 查看状态
systemctl status redis


# 开启远程连接

# 进入并编辑redsi.conf文件
vim /etc/redis.conf

# 找到bind 127.0.0.1 将其注释（#）或修改为 bind 0.0.0.0
bind 0.0.0.0

# 为了安全，我们需要开启密码保护  好好利用vim命令，/requirepass查看单词并跳到这里，进行修改
# 找到 # requirepass xxx ，默认是被注释的，将注释符号去掉，并添加自己的密码
# 找到它要往下拉很久，我们也可以直接在 bind 0.0.0.0 下面添加一个 requirepass xxx
requirepass 123456

# 按 esc 键，并输入 :wq 保存

# 重启，让配置生效
systemctl restart redis
```
## 可视化工具
官网下载RedisInsight