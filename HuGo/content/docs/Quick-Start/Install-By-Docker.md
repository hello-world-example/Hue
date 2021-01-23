# Docker 方式安装



## 配置模板

> https://github.com/cloudera/hue/blob/master/desktop/conf.dist/hue.ini

```bash
$ mkdir -p /private/docker/volumes/hue/conf/
$ cd /private/docker/volumes/hue/conf/
$ wget https://github.com/cloudera/hue/blob/master/desktop/conf.dist/hue.ini
```



## 启动

```bash
$ docker pull gethue/hue:4.8.0

$ docker run -d --name hue \
	-p 8888:8888 \
	-v /private/docker/volumes/hue/conf/hue.ini:/usr/share/hue/desktop/conf/hue.ini \
	gethue/hue:4.8.0
```



## 修改 hue.ini

> 修改配置后需要 `docker restart hue` 重启 hue

```ini
[desktop]
  # https://docs.gethue.com/administrator/configuration/server/#specifying-the-secret-key
  secret_key=jFE93j;2[290-eiw.KEiwN2s3['d;/.q[eIW^y#e=+Iei*@Mn<qW5o
 ...
  http_host=0.0.0.0
  http_port=8888
...
  # 时区
  time_zone=Asia/Shanghai
...
	# 禁用应用
	app_blacklist=pig,hive,impala,druid,spark,spark2,mapreduce,sqoop1,presto,clickhouse,vertica,solr
...
	enable_prometheus=true
	
	[[custom]]
		# 自定义 banner
		## banner_top_html=
		# 登陆提示
		## login_splash_html=
		# 登陆 Logo
		## logo_svg=
		
  [[auth]]
  	# 无需登陆： desktop.auth.backend.AllowAllBackend
  	# 默认第一次登陆创建用户
  	backend=desktop.auth.backend.AllowFirstUserDjangoBackend
```



## Read More

- https://docs.gethue.com/quickstart/
- [Hue Configuration Server](https://docs.gethue.com/administrator/configuration/server/)