#clean will remove running containers and server config
#sterile will clean, then remove ALL volumes and ALL images- even unrelated ones

NAME = diet

ROOT = ${abspath ../..}
RUNTIME = ${ROOT}/runtime
IMAGES = ${ROOT}/config/images
COMPOSITIONS = ${ROOT}/config/compositions

INSTANCE = ${RUNTIME}/${NAME}

VOLUMES = ${RUNTIME}/volumes/${NAME}
SOURCE = ${ROOT}/source

export PATH := ${abspath ${ROOT}/runtime/bin/}:${PATH}

default: cplex instance

cplex: ${IMAGES}/cplex/Dockerfile 
	docker build --tag gp/cplex ${IMAGES}/cplex

instance: volumes_link config deploy

volumes_link: ${INSTANCE}/volumes  

${INSTANCE}/volumes: ${VOLUMES} ${INSTANCE}  
	ln -sf ${VOLUMES} ${INSTANCE}/volumes 

${VOLUMES}:
	mkdir ${VOLUMES}

${INSTANCE}:
	mkdir ${INSTANCE}

config: ${COMPOSITIONS}/runtime.yml ${COMPOSITIONS}/cplex     
	cp ${COMPOSITIONS}/runtime.yml ${INSTANCE}
	cp -r ${COMPOSITIONS}/cplex ${INSTANCE} 

deploy:
	cp -rf ${SOURCE}/* ${VOLUMES}

clean:
	rm -rf ${INSTANCE}
	exec docker-clean

sterile: clean
	exec docker-rmi
	rm -r ${VOLUMES}

