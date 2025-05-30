# Use a stable, multi-arch compatible Java runtime image
FROM eclipse-temurin:17-jre-jammy

# Define build-time arguments for flexibility
ARG SERVICE_USER=jenkins
ARG SERVICE_GROUP=docker
ARG JAR_FILE=target/carts.jar
ARG BUILD_DATE
ARG BUILD_VERSION
ARG COMMIT

# Create group and user for running the service
RUN groupadd --system $SERVICE_GROUP && \
    useradd --system --no-create-home --gid $SERVICE_GROUP $SERVICE_USER

# Set working directory
WORKDIR /kotharepritesh/shopping-carts

# Copy the built JAR from the build context
COPY ${JAR_FILE} ./app.jar

# Adjust permissions
RUN chown $SERVICE_USER:$SERVICE_GROUP ./app.jar

# Switch to non-root user
USER $SERVICE_USER

# Add metadata as labels
LABEL org.label-schema.vendor="Weaveworks" \
      org.label-schema.build-date="${BUILD_DATE}" \
      org.label-schema.version="${BUILD_VERSION}" \
      org.label-schema.name="Socks Shop: Cart" \
      org.label-schema.description="REST API for Cart service" \
      org.label-schema.url="https://github.com/microservices-demo/carts" \
      org.label-schema.vcs-url="github.com:microservices-demo/carts.git" \
      org.label-schema.vcs-ref="${COMMIT}" \
      org.label-schema.schema-version="1.0"

# Run the JAR with a default port
ENTRYPOINT ["java", "-jar", "./app.jar", "--port=80"]
