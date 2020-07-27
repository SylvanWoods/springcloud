# (3) Eureka服务注册与发现

1. 新建springcloud-eureka-server服务,并设置相关配置

+ 右键父工程新建名为springcloud-eureka-server的module工程，新建完成之后项目结构为如下所示

  ```markdown
    | - springcloud
    		| - springcloud-eureka-server
    				| - src
    				| - pom.xml
    		| - pom.xml
  ```

+ 修改pom.xml继承至父pom文件

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
  
  
      <artifactId>springcloud-eureka</artifactId>
      <name>springcloud-eureka</name>
      <description>Demo project for Spring Boot</description>
  		
      <!--修改此处parent修改为父pom-->
      <parent>
          <groupId>com.sylvan.springcloud</groupId>
          <artifactId>springcloud</artifactId>
          <version>0.0.1-SNAPSHOT</version>
      </parent>
  
  
      <properties>
          <java.version>1.8</java.version>
      </properties>
  
      <dependencies>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
  
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
              <optional>true</optional>
          </dependency>
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
              <exclusions>
                  <exclusion>
                      <groupId>org.junit.vintage</groupId>
                      <artifactId>junit-vintage-engine</artifactId>
                  </exclusion>
              </exclusions>
          </dependency>
      </dependencies>
  
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

+ 在我们使用spring cloud之前，我们需要去spring cloud官网查看一下最新版本信息

  ```markdown
  访问网址：https://spring.io/projects/spring-cloud/
  在最下面可以看到
  
  ```

  

+ 在父pom.xml中引入spring cloud版本,我这里使用的是Hoxton SR6版本

  ``` xml
  <?xml version="1.0" encoding="UTF-8"?>
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <parent>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-parent</artifactId>
          <version>2.3.2.RELEASE</version>
          <relativePath/> <!-- lookup parent from repository -->
      </parent>
  
      <groupId>com.sylvan.springcloud</groupId>
      <artifactId>springcloud</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <name>springcloud</name>
      <description>parent project</description>
      <packaging>pom</packaging>
  
      <properties>
          <java.version>1.8</java.version>
          <lombok.version>1.18.12</lombok.version>
          <springboot.version>2.3.2.RELEASE</springboot.version>
          <springcloud.version>Hoxton SR6</springcloud.version>
      </properties>
  
  
      <dependencyManagement>
          <dependencies>
              <dependency>
                  <groupId>org.springframework.cloud</groupId>
                  <artifactId>spring-cloud-dependencies</artifactId>
                  <version>${springcloud.version}</version>
                  <type>pom</type>
                  <scope>import</scope>
              </dependency>
  
              <dependency>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-starter-web</artifactId>
                  <version>${springboot.version}</version>
              </dependency>
  
              <dependency>
                  <groupId>org.projectlombok</groupId>
                  <artifactId>lombok</artifactId>
                  <version>${lombok.version}</version>
                  <scope>provided</scope>
              </dependency>
  
              <dependency>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-starter-test</artifactId>
                  <version>${springboot.version}</version>
                  <scope>test</scope>
                  <exclusions>
                      <exclusion>
                          <groupId>org.junit.vintage</groupId>
                          <artifactId>junit-vintage-engine</artifactId>
                      </exclusion>
                  </exclusions>
              </dependency>
          </dependencies>
      </dependencyManagement>
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

  

+ 在pom.xml中新增maven，eureka server依赖

  ```markdown
     <!--eureka 服务端-->
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
              <version>2.2.3.RELEASE</version>
          </dependency>
  ```



1. 新建springcloud-eureka-client服务