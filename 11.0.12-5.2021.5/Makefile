ZULU_VERSION=11.0.12
PAYARA_VERSION=5
PAYARA_RELEASE=2021.5
PAYARA_TAG=${PAYARA_VERSION}.${PAYARA_RELEASE}

image:
	docker build --build-arg ZULU_VERSION=${ZULU_VERSION} --build-arg PAYARA_TAG=${PAYARA_TAG} --build-arg PAYARA_RELEASE=${PAYARA_RELEASE} -t distroless-zulu-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} .
	@echo ""
	@echo "To test the image run:"
	@echo "docker run -it --rm --cpus 2 --memory 640m distroless-zulu-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}"

tag-and-push: image
	docker tag distroless-zulu-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} qaware/distroless-zulu-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}
	docker push qaware/distroless-zulu-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}

latest: tag-and-push
	docker tag distroless-zulu-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} qaware/distroless-zulu-payara-micro:latest
	docker push qaware/distroless-zulu-payara-micro:latest
