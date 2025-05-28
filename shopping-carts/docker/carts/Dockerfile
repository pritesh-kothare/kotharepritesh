# Use a stable, multi-arch compatible Java runtime image
FROM eclipse-temurin:17-jre-jammy

ARG SERVICE_USER=jenkins
ARG SERVICE_GROUP=docker

RUN groupadd --system $SERVICE_GROUP && \
    useradd --system --no-create-home --gid $SERVICE_GROUP $SERVICE_USER

WORKDIR /usr/src/app

ARG JAR_FILE=target/cart-service-1.0.0.jar

# CORRECT: Copy from the `target/` directory
COPY ${JAR_FILE} ./app.jar

RUN chown $SERVICE_USER:$SERVICE_GROUP ./app.jar

USER $SERVICE_USER

ARG BUILD_DATE
ARG BUILD_VERSION
ARG COMMIT

LABEL org.label-schema.vendor="Weaveworks" \
      org.label-schema.build-date="${BUILD_DATE}" \
      org.label-schema.version="${BUILD_VERSION}" \
      org.label-schema.name="Socks Shop: Cart" \
      org.label-schema.description="REST API for Cart service" \
      org.label-schema.url="https://github.com/microservices-demo/carts" \
      org.label-schema.vcs-url="github.com:microservices-demo/carts.git" \
      org.label-schema.vcs-ref="${COMMIT}" \
      org.label-schema.schema-version="1.0"

ENTRYPOINT ["java", "-jar", "./app.jar", "--port=80"]
