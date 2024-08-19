## Redis

### Redis 部署

1. 在 root 目录下创建以下目录，准备与 Redis 容器进行挂载
~~~linux
mkdir -p redis/{conf,data,log}
~~~
2. 在 conf 目录下编辑 redis.conf 配置文件
~~~conf
# redis.conf
# 监听地址
bind 127.0.0.1
# 端口
port 6379
# 密码
requirepass 123321
# 不允许守护进程模式(设置允许与参数-d冲突，容器无法启动)
daemonize no
# 禁用保护模式
protected-mode no
~~~
3. 运行 docker 命令部署 Redis 容器
~~~linux
docker run \
--restart=always \
--log-opt max-size=100m \
--log-opt max-file=2 \
--name my-redis -d \
-p 6379:6379 \
-v ./redis/data:/data \
-v ./redis/conf/redis.conf:/usr/local/etc/redis/redis.conf \
-v ./redis/log:/var/log/redis \
redis redis-server /usr/local/etc/redis/redis.conf
~~~
4. 以终端的形式访问 Redis
~~~
docker exec -it my-redis redis-cli
~~~
