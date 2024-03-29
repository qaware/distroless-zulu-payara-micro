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

RUN rm -rf /usr/lib/jvm/zulu11/src.zip && \
 rm -rf /usr/lib/jvm/zulu11/sample/ && \
 rm -rf /usr/lib/jvm/zulu11/demo/

ARG PAYARA_TAG
ARG PAYARA_RELEASE

ENV PAYARA_PKG https://search.maven.org/remotecontent?filepath=fish/payara/extras/payara-micro/$PAYARA_TAG/payara-micro-$PAYARA_TAG.jar
ENV PAYARA_VERSION $PAYARA_RELEASE
ENV PKG_FILE_NAME payara-micro.jar

RUN curl --silent --location --show-error --output $PAYARA_PATH/$PKG_FILE_NAME $PAYARA_PKG

FROM gcr.io/distroless/base
LABEL maintainer="qaware-oss@qaware.de"

ENV JAVA_HOME /usr/lib/jvm/zulu11
ENV PAYARA_PATH /opt/payara
ENV DEPLOY_DIR $PAYARA_PATH/deployments
ENV AUTODEPLOY_DIR $PAYARA_PATH/deployments

ENV ENV="/etc/profile"
COPY etc_profile /etc/profile

COPY --from=build /etc/passwd /etc/passwd
COPY --from=build /etc/group /etc/group

COPY --from=amd64/busybox:1.34.0 /bin/busybox /busybox/busybox
RUN ["/busybox/busybox", "--install", "/bin"]

USER payara
WORKDIR $PAYARA_PATH

COPY --from=build $PAYARA_PATH $PAYARA_PATH
COPY --from=build $JAVA_HOME $JAVA_HOME
COPY --from=build /usr/lib64/libz.* /lib/x86_64-linux-gnu/

# Default payara ports to expose
EXPOSE 8080 8443 6900

ENTRYPOINT ["/usr/lib/jvm/zulu11/bin/java", "-server", "-Xshare:on", "-XX:+UseContainerSupport", "-XX:MaxRAMPercentage=50.0", "-XX:ThreadStackSize=256", "-XX:MaxMetaspaceSize=128m", "-XX:+UseShenandoahGC", "-XX:+AlwaysPreTouch", "-XX:+UseNUMA", "-XX:+UseStringDeduplication", "-jar", "/opt/payara/payara-micro.jar"]
CMD ["--nocluster", "--disablephonehome", "--deploymentDir", "/opt/payara/deployments"]
