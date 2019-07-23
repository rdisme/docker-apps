# docker-envs
用docker构建的项目环境


## 目录结构

> [v1](#v1)
>> nginx + python

> [v2](#v2)
>> nginx + php + mysql


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
