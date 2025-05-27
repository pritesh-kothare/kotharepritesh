# ✅ Use a multi-arch compatible Java image
FROM eclipse-temurin:17-jre-alpine
# Define user and group via build arguments
ARG SERVICE_USER=myuser
ARG SERVICE_GROUP=mygroup

# Create the user and group
RUN addgroup -S $docker && adduser -S $jemnkins -G $docker

# Set working directory
WORKDIR /usr/src/app

# Copy the JAR file into the image
COPY *.jar ./app.jar

# Set permissions
RUN chown -R $SERVICE_USER:$SERVICE_GROUP ./app.jar

# Switch to the created user
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
