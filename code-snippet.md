# code-snippet

# 1
```
buildscript {
    ... ...
    dependencies {
        classpath('se.transmode.gradle:gradle-docker:1.2')
    }
}

group 'liuwill'
version '1.0-SNAPSHOT'

... ...
apply plugin: 'docker'

... ...
jar {
    baseName = 'boot-kotlin-app'
    version =  '0.1.0'
}
mainClassName = 'com.liuwill.demo.kotlinBoot.SpringBootKotlinApplicationKt'

task buildDocker(type: Docker, dependsOn: build, group: "custom") {
    push = true
    applicationName = jar.baseName
    dockerfile = file('src/main/docker/Dockerfile')
    doFirst {
        copy {
            from jar
            into stageDir
        }
    }
}
```