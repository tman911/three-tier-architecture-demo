# Build
FROM maven:3.8-openjdk-11 AS build

WORKDIR /opt/shipping

# Copy entire project (pom.xml + src + .mvn if exists)
COPY . .

# Optional: clean first to ensure no caching issues
RUN mvn clean package -DskipTests

# Run
FROM openjdk:8-jdk

EXPOSE 8080

WORKDIR /opt/shipping

ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql

COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar

CMD ["java", "-Xmn256m", "-Xmx768m", "-jar", "shipping.jar"]
