#!/usr/bin/make -f

ifdef LOCAL
VOLUMES=-v /stv/src/edx/xblock/sdk:/xblock/sdk -v /stv/src/edx/xblock/factory:/xblock/factory
endif
TAG=xblock/sdk
NAME=workbench
DOCKER=docker
PORT_HOST=8002
PORT_DOCKER=8002
_docker_run=${DOCKER} run -p ${PORT_DOCKER}:${PORT_HOST} ${VOLUMES}
_docker_run_quick=${_docker_run} -i -t --rm "${TAG}"
_docker_shell=/bin/bash

.PHONY:
all: run

.PHONY:
run: build
	${_docker_run_quick}

.PHONY:
shell: build
	${_docker_run_quick} "${_docker_shell}"

.PHONY:
build: Dockerfile
	${DOCKER} build -t "${TAG}" .

.PHONY:
daemon: build
	${_docker_run} -d --name "${NAME}" "${TAG}"
	echo
	${DOCKER} ps

.PHONY:
stop:
	-${DOCKER} rm -f "${NAME}"

.PHONY:
clean: stop
	-${DOCKER} rmi "${TAG}"
	-${DOCKER} rmi $(shell ${DOCKER} images -qf 'dangling=true')
