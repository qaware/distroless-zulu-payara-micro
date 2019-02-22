ARG ZULU_VERSION
FROM azul/zulu-openjdk-centos:$ZULU_VERSION as build

ENV PAYARA_PATH /opt/payara

RUN yum -q -y install curl && \
 update-ca-trust && \
 useradd -d $PAYARA_PATH payara && echo payara:0 | chpasswd && \
 mkdir -p $PAYARA_PATH/deployments && \
 mkdir -p $PAYARA_PATH/libs && \
 chown -R payara:0 $PAYARA_PATH && \
 java -Xshare:dump

ARG PAYARA_TAG
ARG PAYARA_RELEASE

ENV PAYARA_PKG https://search.maven.org/remotecontent?filepath=fish/payara/extras/payara-micro/$PAYARA_TAG/payara-micro-$PAYARA_TAG.jar
ENV PAYARA_VERSION $PAYARA_RELEASE
ENV PKG_FILE_NAME payara-micro.jar

RUN curl --silent --show-error --output $PAYARA_PATH/$PKG_FILE_NAME $PAYARA_PKG

FROM gcr.io/distroless/base
LABEL maintainer="qaware-oss@qaware.de"

ENV JAVA_HOME /usr/lib/jvm/zulu-8
ENV PAYARA_PATH /opt/payara
ENV DEPLOY_DIR $PAYARA_PATH/deployments
ENV AUTODEPLOY_DIR $PAYARA_PATH/deployments

COPY --from=build /etc/passwd /etc/passwd
COPY --from=build /etc/group /etc/group

USER payara
WORKDIR $PAYARA_PATH

COPY --from=build $PAYARA_PATH $PAYARA_PATH
COPY --from=build $JAVA_HOME $JAVA_HOME

# Default payara ports to expose
EXPOSE 8080 8443 6900

ENTRYPOINT ["/usr/lib/jvm/zulu-8/bin/java", "-server", "-Xshare:on", "-XX:+UnlockExperimentalVMOptions", "-XX:+UseCGroupMemoryLimitForHeap", "-XX:MaxRAMFraction=3", "-XX:ThreadStackSize=256", "-XX:MaxMetaspaceSize=128m", "-XX:+UseG1GC", "-XX:ParallelGCThreads=2", "-XX:CICompilerCount=2", "-XX:+UseStringDeduplication", "-jar", "/opt/payara/payara-micro.jar"]
CMD ["--deploymentDir", "/opt/payara/deployments"]
