# 将官方 Python 运行时用作父镜像
FROM python:3.7

# 将工作目录设置为 /myapp
WORKDIR /myapp

# pip安装软件包
RUN pip install \
		flask \
		redis \
		Django==2.2 \
		uwsgi \
		uwsgitop