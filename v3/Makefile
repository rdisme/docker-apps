# node image version
NODE_VERSION=node:8
# container name
CONTAINER_NAME=node.v3
# local src
HOST_SRC=${PWD}/app
# container src
CONTAINER_DEST=/usr/src/app


run:
	@echo "node version is: "${NODE_VERSION}
	@echo "container name is: "${CONTAINER_NAME}
	@echo "host path is: "${HOST_SRC}
	@echo "===============执行命令===================="
	docker run -it -d \
		-v ${HOST_SRC}:${CONTAINER_DEST} \
		-w ${CONTAINER_DEST} \
		-p 9527:9527 \
		--rm \
		--name ${CONTAINER_NAME} ${NODE_VERSION}