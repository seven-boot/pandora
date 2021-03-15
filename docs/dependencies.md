## 约定

- 所有 pom 文件中的依赖声明放在`<dependencies>`语句块中，所有版本声明放在`<dependencyManagement>`语句块中。
  - 说明：`<dependencyManagement>` 里只是声明版本，并不实现引入，所有子项目需要显式的声明依赖，version 和 scope 都读取自父 pom，而 `<dependencies>` 所有声明在主 pom 的 `<dependencies>` 里的依赖都会自动引入，并默认被所有的子项目继承。

### pandora-dependencies

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.seven.pandora</groupId>
    <artifactId>pandora-dependencies</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <packaging>pom</packaging>

    <name>pandora-dependencies</name>
    <description>统一的依赖管理</description>

    <scm>
        <connection>scm:git:https://github.com/seven-boot/pandora-dependencies.git</connection>
        <developerConnection>scm:git:https://github.com/seven-boot/pandora-dependencies.git</developerConnection>
        <url>https://github.com/seven-boot/pandora-dependencies</url>
    </scm>

    <properties>
        <java.version>1.8</java.version>
        <maven.compiler.source>${java.version}</maven.compiler.source>
        <maven.compiler.target>${java.version}</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>

        <!-- Spring Projects -->
        <spring-boot.version>2.3.1.RELEASE</spring-boot.version>
        <spring-cloud.version>Hoxton.SR4</spring-cloud.version>
        <spring-cloud-alibaba.verion>2.2.1.RELEASE</spring-cloud-alibaba.verion>
        <spring-context-support.version>1.0.6</spring-context-support.version>
        <mybatis-spring-boot-starter.version>2.1.2</mybatis-spring-boot-starter.version>
        <pagehelper-spring-boot-starter.version>1.2.13</pagehelper-spring-boot-starter.version>
        <knife4j-spring-boot-starter.version>2.0.3</knife4j-spring-boot-starter.version>

        <!-- Dubbo Projects -->
        <dubbo.version>2.7.7</dubbo.version>
        <dubbo-nacos.version>1.3.0</dubbo-nacos.version>

        <!-- Projects -->
        <okhttp.version>3.14.9</okhttp.version>
        <easy-captcha.version>1.6.2</easy-captcha.version>
        <pandora.version>1.0.0.RELEASE</pandora.version>
        <pandora.development.version>1.0.1-SNAPSHOT</pandora.development.version>
    </properties>

    <licenses>
        <license>
            <name>Apache 2.0</name>
            <url>https://www.apache.org/licenses/LICENSE-2.0.txt</url>
        </license>
    </licenses>

    <developers>
        <developer>
            <name>seven</name>
            <email>H_Qiao1126@163.com</email>
        </developer>
    </developers>

    <distributionManagement>
        <repository>
            <id>nexus-releases</id>
            <url>http://192.168.80.69:18018/repository/maven-releases/</url>
        </repository>
        <snapshotRepository>
            <id>nexus-snapshots</id>
            <url>http://192.168.80.69:18018/repository/maven-snapshots/</url>
        </snapshotRepository>
    </distributionManagement>

    <dependencyManagement>
        <dependencies>
            <!-- Spring Boot -->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>${spring-boot.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>

            <!-- Spring Cloud -->
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>

            <!-- Spring Cloud Alibaba -->
            <dependency>
                <groupId>com.alibaba.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>${spring-cloud-alibaba.verion}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>

            <!-- Dubbo Dependencies -->
            <dependency>
                <groupId>org.apache.dubbo</groupId>
                <artifactId>dubbo-dependencies-bom</artifactId>
                <version>${dubbo.version}</version>
                <type>pom</type>
                <scope>import</scope>
                <exclusions>
                    <exclusion>
                        <groupId>org.springframework</groupId>
                        <artifactId>spring-framework-bom</artifactId>
                    </exclusion>
                </exclusions>
            </dependency>

            <!-- Apache Dubbo -->
            <dependency>
                <groupId>org.apache.dubbo</groupId>
                <artifactId>dubbo-spring-boot-starter</artifactId>
                <version>${dubbo.version}</version>
            </dependency>
            <dependency>
                <groupId>org.apache.dubbo</groupId>
                <artifactId>dubbo-registry-nacos</artifactId>
                <version>${dubbo.version}</version>
            </dependency>
            <dependency>
                <groupId>org.apache.dubbo</groupId>
                <artifactId>dubbo</artifactId>
                <version>${dubbo.version}</version>
                <exclusions>
                    <exclusion>
                        <groupId>org.springframework</groupId>
                        <artifactId>spring</artifactId>
                    </exclusion>
                    <exclusion>
                        <groupId>javax.servlet</groupId>
                        <artifactId>servlet-api</artifactId>
                    </exclusion>
                    <exclusion>
                        <groupId>log4j</groupId>
                        <artifactId>log4j</artifactId>
                    </exclusion>
                </exclusions>
            </dependency>
            <dependency>
                <groupId>org.apache.dubbo</groupId>
                <artifactId>dubbo-spring-boot-actuator</artifactId>
                <version>${dubbo.version}</version>
            </dependency>
            <dependency>
                <groupId>org.apache.dubbo</groupId>
                <artifactId>dubbo-serialization-kryo</artifactId>
                <version>${dubbo.version}</version>
                <exclusions>
                    <exclusion>
                        <groupId>log4j</groupId>
                        <artifactId>log4j</artifactId>
                    </exclusion>
                    <exclusion>
                        <groupId>org.apache.dubbo</groupId>
                        <artifactId>dubbo-common</artifactId>
                    </exclusion>
                </exclusions>
            </dependency>
            <dependency>
                <groupId>com.alibaba.spring</groupId>
                <artifactId>spring-context-support</artifactId>
                <version>${spring-context-support.version}</version>
            </dependency>

            <!-- Mybatis -->
            <dependency>
                <groupId>org.mybatis.spring.boot</groupId>
                <artifactId>mybatis-spring-boot-starter</artifactId>
                <version>${mybatis-spring-boot-starter.version}</version>
            </dependency>
            <dependency>
                <groupId>com.github.pagehelper</groupId>
                <artifactId>pagehelper-spring-boot-starter</artifactId>
                <version>${pagehelper-spring-boot-starter.version}</version>
            </dependency>
            <dependency>
                <groupId>com.github.xiaoymin</groupId>
                <artifactId>knife4j-micro-spring-boot-starter</artifactId>
                <version>${knife4j-spring-boot-starter.version}</version>
            </dependency>
            <dependency>
                <groupId>com.github.xiaoymin</groupId>
                <artifactId>knife4j-spring-boot-starter</artifactId>
                <version>${knife4j-spring-boot-starter.version}</version>
            </dependency>

            <!--    Commons        -->
            <dependency>
                <groupId>com.github.whvcse</groupId>
                <artifactId>easy-captcha</artifactId>
                <version>${easy-captcha.version}</version>
            </dependency>
            <dependency>
                <groupId>com.squareup.okhttp3</groupId>
                <artifactId>okhttp</artifactId>
                <version>${okhttp.version}</version>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <!-- Maven 多环境配置 -->
    <profiles>
        <profile>
            <id>default</id>
            <activation>
                <activeByDefault>true</activeByDefault>
            </activation>
            <properties>
                <maven-release-plugin.version>2.5.3</maven-release-plugin.version>
                <maven-scm-provider-jgit-plugin.version>1.9.5</maven-scm-provider-jgit-plugin.version>
                <spring-javaformat-maven-plugin.version>0.0.22</spring-javaformat-maven-plugin.version>
            </properties>
            <build>
                <plugins>
                    <plugin>
                        <groupId>io.spring.javaformat</groupId>
                        <artifactId>spring-javaformat-maven-plugin</artifactId>
                        <version>${spring-javaformat-maven-plugin.version}</version>
                    </plugin>

                    <plugin>
                        <groupId>org.apache.maven.plugins</groupId>
                        <artifactId>maven-release-plugin</artifactId>
                        <version>${maven-release-plugin.version}</version>
                        <configuration>
                            <providerImplementations>
                                <git>jgit</git>
                            </providerImplementations>
                            <username>seven-boot</username>
                            <password>qiaohao1126</password>
                            <tagBase>${project.artifactId}-${project.version}</tagBase>
                            <goals>-f pom.xml deploy</goals>
                            <releaseLabel>${pandora.version}</releaseLabel>
                            <releaseVersion>${pandora.version}</releaseVersion>
                            <developmentVersion>${pandora.development.version}</developmentVersion>
                            <preparationGoals>clean verify</preparationGoals>
                            <checkModificationExcludes>
                                <checkModificationExclude>*.iml</checkModificationExclude>
                            </checkModificationExcludes>
                        </configuration>
                        <dependencies>
                            <dependency>
                                <groupId>org.apache.maven.scm</groupId>
                                <artifactId>maven-scm-provider-jgit</artifactId>
                                <version>${maven-scm-provider-jgit-plugin.version}</version>
                            </dependency>
                        </dependencies>
                    </plugin>
                </plugins>
            </build>
        </profile>
    </profiles>
</project>
```

