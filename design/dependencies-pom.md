# Dependencies POM

## 内容

### 属性定义

dreamfly-dependencies 中定义了大量的属性(property)，主要用来定义各种版本：

```xml
<properties>
	<java.version>1.8</java.version>
	<guava.version>19.0</guava.version>
	......
```

### dependencyManagement 定义

定义了大量的第三方依赖，其中版本通过上面定义的属性/properties 来统一管理：

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.google.guava</groupId>
            <artifactId>guava</artifactId>
            <version>${guava.version}</version>
        </dependency>
        ......
    </dependencies>
</dependencyManagement>
```

### extension 定义

目前只有一个 extendsion 需要公用，即 `os-maven-plugin`：

```xml
<build>
        <extensions>
            <extension>
                <groupId>kr.motd.maven</groupId>
                <artifactId>os-maven-plugin</artifactId>
                <version>${os-maven-plugin.version}</version>
            </extension>
        </extensions>
        ......
</build>
```

### pluginManagement 定义

pluginManagement 定义好插件信息，尤其是版本：

```xml
<pluginManagement>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-surefire-plugin</artifactId>
                    <version>${maven.surefire.plugin.version}</version>
                </plugin>

        		......
            </plugins>
</pluginManagement>
```


