# Use a stable, multi-arch compatible Java runtime image
FROM eclipse-temurin:17-jre-jammy

# Define user and group via build arguments
ARG SERVICE_USER=jenkins
ARG SERVICE_GROUP=docker

# Create the user and group (Ubuntu-compatible)
RUN groupadd --system $SERVICE_GROUP && \
    useradd --system --no-create-home --gid $SERVICE_GROUP $SERVICE_USER

# Set the working directory
WORKDIR /usr/src/app

# Accept the JAR file as a build argument (flexible for CI/CD)
ARG JAR_FILE=app.jar

# Copy the JAR file into the image
COPY ${JAR_FILE} ./app.jar

# Set correct ownership for the application file
RUN chown $SERVICE_USER:$SERVICE_GROUP ./app.jar

# Switch to the created unprivileged user
USER $SERVICE_USER

# Add build metadata
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

# Start the Java app
ENTRYPOINT ["java", "-jar", "./app.jar", "--port=80"]
