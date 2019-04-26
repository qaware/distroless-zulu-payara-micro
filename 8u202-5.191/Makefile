ZULU_VERSION=8u202
PAYARA_VERSION=5
PAYARA_RELEASE=191
PAYARA_TAG=${PAYARA_VERSION}.${PAYARA_RELEASE}

image:
	docker build --build-arg ZULU_VERSION=${ZULU_VERSION} --build-arg PAYARA_TAG=${PAYARA_TAG} --build-arg PAYARA_RELEASE=${PAYARA_RELEASE} -t distroless-zulu-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} .

tag-and-push: image
	docker tag distroless-zulu-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} qaware/distroless-zulu-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}
	docker push qaware/distroless-zulu-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}

latest: tag
	docker tag distroless-zulu-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} qaware/distroless-zulu-payara-micro:latest
	docker push qaware/distroless-zulu-payara-micro:latest
