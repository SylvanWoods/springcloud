# （1）idea新建多module模块项目

+ 首先新建一个Project项目

  ```markdown
  新建project项目 
  1. File --> new --> Project
  2. 选择Spring Initializr --> Project SDK(选择你本机安装的java JDK)--> 点击下一步，然后按照需求配置好相关参数,目录结构如下。
      | - springcloud
  3. Project新建并配置好以后，删除相关Src目录，仅保留POM.XML即可,目录结构如下
      | - springcloud
          | - pom.xml
    其中pom.xml的<packaging>标签应修改为pom。
    注意: 
     a. pom.xml中的packaging标签修改为pom后，其管理<dependencies>标签的父标签为<dependencyManagement>。      
     b. <dependency>标签并非为实际导入的相关jar包，而是一种定义，用于统一各子模块（module）中的版本信息，具体获取包还是需要在module项目中获取。如果module中未自定义版本则使用父POM定义的版本信息。其主要目的为方便管理版本信息。
    
  ```

  + 父pom.xml如下

  ```xml
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
      </properties>
  
      <dependencyManagement>
          <dependencies>
              <dependency>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-starter-web</artifactId>
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

+ 新建module模块项目

  ```markdown
  选中Project项目名并右键选择 --》 New --》 Module,新建Module流程与新建Project一样,创建完成目录结构如下，我这里创建了多个module项目。
      | - springcloud
      	  | - springcloud-client
      	  | - springcloud-eureka
      	  | - springcloud-service
          | - pom.xml
  ```

+ 总结

  ~~~markdown
  这种方式的好处是，当我们开发多模块的项目的时，如果没有一个集中统一管理的父项目。那么势必会造成，版本混乱，项目混乱等等，不利于后期开发维护等。通过父项目对所有子项目相关依赖包的版本管理，达到一个统一的处理和修改，即当需要升级版本时，一个地方修改即可。
  ~~~

  

