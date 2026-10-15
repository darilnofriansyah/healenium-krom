FROM maven:3.9.9-eclipse-temurin-21 AS build
WORKDIR /workspace
RUN git init . \
    && git remote add origin https://github.com/healenium/healenium-proxy.git \
    && git fetch --depth 1 origin c31320b5d747d65f2731ba93745fe036100041bf \
    && git checkout --detach FETCH_HEAD
COPY docker/healenium-proxy/selenium-4.27.patch /tmp/selenium-4.27.patch
RUN git apply /tmp/selenium-4.27.patch \
    && mvn -B -ntp clean package

FROM eclipse-temurin:23
COPY --from=build /workspace/target/hlm-proxy-2.2.1.jar /hlm-proxy.jar
EXPOSE 8085
CMD ["java", "-jar", "/hlm-proxy.jar"]
