# 配置项目结构

当默认的项目结构不适用时，可以自定义配置。查看 Gradle 文档中 [Java plugin][1] 部分以了解如何在纯 Java 项目中进行配置。

Android plugin 使用了类似的语法，但因为 Android 有自己的 *sourceSets*，所以需要配置到 **<font color='green'>android</font>** 块中。下面的例子使用了旧的项目结构(Eclipse)，并把 **<font color='green'>androidTest</font>** 的 *sourceSet* 映射到 tests 目录中。

``` Groovy
android {
    sourceSets {
        main {
            manifest.srcFile 'AndroidManifest.xml'
            java.srcDirs = ['src']
            resources.srcDirs = ['src']
            aidl.srcDirs = ['src']
            renderscript.srcDirs = ['src']
            res.srcDirs = ['res']
            assets.srcDirs = ['assets']
        }

        androidTest.setRoot('tests')
    }
}
```

> 注意：因为旧的结构把所有的源文件（Java, AIDL, Renderscript）放在同一个目录中，所以我们需要重新映射所有的 *sourceSet* 新组件到同一个 **<font color='green'>src</font>** 目录下。

> 注意：**<font color='green'>setRoot()</font>** 会移动所有的 sourceSet（包括它的子目录）到新的目录。例子中把 **<font color='green'>src/androidTest/*</font>** 移动到 **<font color='green'>tests/*</font>**

Android 特有的 *sourceSets* 在 Java *sourceSets* 中不起作用。

[1]: http://gradle.org/docs/current/userguide/java_plugin.html