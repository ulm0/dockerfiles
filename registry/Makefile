DOCKER_IMAGE_VERSION=2
DOCKER_IMAGE_NAME=$(CI_REGISTRY_IMAGE)
DOCKER_IMAGE_TAGNAME=$(DOCKER_IMAGE_NAME):$(DOCKER_IMAGE_VERSION)

ifeq ($(CI_REGISTRY_IMAGE),)
	DOCKER_IMAGE_NAME=ulm0/registry
endif

default: dist docker clean

dist: bin
	@./ci/dist

bin:
	mkdir bin

compress: 
	upx -qq --best bin/registry

docker: image push

image: compress
	docker build -t $(DOCKER_IMAGE_TAGNAME)-$(REG_ARCH) .

clean:
	rm -rf ./bin

push:
	docker push $(DOCKER_IMAGE_TAGNAME)-$(REG_ARCH)

test:
	docker run --rm $(DOCKER_IMAGE_TAGNAME)-$(REG_ARCH) --version
