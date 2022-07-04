# Pom files in spring boot

The parent pom.xml:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!-- CHANGE STUFF HERE -->
  <groupId>org.yohan</groupId>
  <artifactId>micro-backend</artifactId>
  <packaging>pom</packaging>
  <version>1.0-SNAPSHOT</version>

  <!-- LIST OF MODULES (child dependencies) -->
  <modules>
    <module>customer</module>
    <module>fraud</module>
    <module>eureka-server</module>
    <module>clients</module>
    <module>notification</module>
    <module>gateway</module>
    <module>amqp</module>
  </modules>

  <!-- CHANGE STUFF HERE -->
  <name>micro-backend</name>
  <url>https://github.com/searoll</url>

  <!-- CHANGE STUFF HERE -->
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>
  </properties>

  <!-- DO NOT CHANGE ANYTHING HERE -->
  <dependencyManagement>
    <dependencies>
      <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-dependencies</artifactId>
        <version>2.7.0</version>
        <scope>import</scope>
        <type>pom</type>
      </dependency>
    </dependencies>
  </dependencyManagement>

  <!-- dependencies used over all services -->
  <dependencies>
    <dependency>
      <groupId>org.projectlombok</groupId>
      <artifactId>lombok</artifactId>
      <version>1.18.24</version>
    </dependency>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-test</artifactId>
      <version>2.7.0</version>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-openfeign</artifactId>
      <version>3.1.3</version>
    </dependency>
  </dependencies>

  <!-- build plugins. don't change -->
  <build>
    <pluginManagement>
      <plugins>
        <plugin>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-maven-plugin</artifactId>
          <executions>
            <execution>
              <goals>
                <goal>repackage</goal>
              </goals>
            </execution>
          </executions>
        </plugin>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.10.1</version>
          <configuration>
            <source>17</source>
            <target>17</target>
          </configuration>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>
```

any child pom.xml should have these:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- PARENT NAME -->
    <parent>
        <groupId>org.yohan</groupId>
        <artifactId>micro-backend</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>

    <!-- Service name -->
    <groupId>com.yohan</groupId>
    <artifactId>fraud</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>fraud</name>
    <description>fraud</description>

    <!-- Service java version -->
    <properties>
        <java.version>17</java.version>
    </properties>

    <!-- Dependencies used per service -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
            <version>3.1.3</version>
        </dependency>

        <!-- feign clients -->
        <dependency>
            <groupId>org.yohan</groupId>
            <artifactId>clients</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-sleuth</artifactId>
            <version>3.1.3</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-sleuth-zipkin</artifactId>
        </dependency>
    </dependencies>

    <!-- made for building jar files DONT CHANGE -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

inside the application.yml, these are recommended:

```yaml
zipkin:
  base-url: http://zipkin:9411
```
