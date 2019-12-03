# docker-envs

> 建议

- 推荐使用vs code编辑器，安装docker扩展，方便管理容器与镜像
- [配置daocloud镜像站](https://www.daocloud.io/mirror)

> Install Docker

- [Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)

- [Windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows)

- [Linux](https://docs.docker.com/install/linux/docker-ce/centos/)

> Docker document

- [官方文档](https://docs.docker.com/install/linux/docker-ce/centos/)


## 目录结构

> [v1](#v1)
>> nginx + python

> [v2](#v2)
>> nginx + php + mysql + redis + rabbitmq

> [v3](#v3)
>> nodejs 环境


## <span id='v1'>v1</span>

进入目录，执行
```
docker-compose up
````
1、python.default, uWSGU服务启动
```
loalhost:8000
````
2、python.mysite，Django项目
```
loalhost
````
3、python.testsite，Django项目（模拟nginx配置多项目）
```
loalhost:81
````

## <span id='v2'>v2<span>

进入目录，执行
```
docker-compose up
````
安装完毕之后，就可以通过浏览器访问 localhost，会打印phpinfo


## <span id='v3'>v3</span>
nodejs 环境

> app ：项目目录，所有的前端代码需要在这个目录下完成

> Makefile ： node环境核心文件，请务必查看！！！

执行如下命令，启动docker容器
```
make run
```
若是本地没有make命令，只能执行：
```
docker run -it -d \
		-v ${HOST_SRC}:${CONTAINER_DEST} \
		-w ${CONTAINER_DEST} \
		-p 9527:9527 \
		--rm \
		--name ${CONTAINER_NAME} ${NODE_VERSION}
```

工作模式：
- 在app目录下更新代码
- 需要进入容器中执行 npm等一些列命令

进入容器命令（若是vs code编辑器，容器管理会更方便）
```
docker exec -it 容器名 /bin/bash
```