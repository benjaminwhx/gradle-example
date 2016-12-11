# Gradle命令行详解

## 1、探索task

| 名字 | 描述 |
|--------|--------|
|dependencies |列出你的项目依赖,包括传递性依赖。 |
|dependencyInsight |解释在依赖图中一个依赖如何被选择,为什么被选择。检查一个特定的依赖,需要提供--dependency参数。检查compile依赖以外的依赖,使用--configuration参数。如: gradle dependencyInsight --dependency apache-commons。 |
|help |显示Gradle命令行的基本语法;比如,列出所有task和运行一个特定的task。如果你运行gradle命令而未指定任何task,help task就会被自动执行。 |
|projects |显示在多项目构建中的所有子项。单项目构建没有子项目。 |
|properties |列出项目中所有可用的属性。有些属性是由Gradle的Project对象提供的。其他属性是用户自定义的属性,可能来自于属性文件、属性命令行选项,或者直接在构建脚本中定义的。 |
|tasks |显示项目中所有可运行的task,包括它们的描述信息。引用于项目的插件提供了额外的task。显示可用的task的附加信息,可以使用--all选项。 |

## 2、构建设置task

| 名字 | 描述 |
|--------|--------|
|setupBuild |通过创建build.gradle和settings.gradle来初始化一个Gradle项目,设置wrapper文件。如果Gradle找到了一个pom.xml文件,Gradle会尝试从这个Maven基本数据中继承项目信息(参考maven2Gradle) |
|generateBuildFile |为构建java项目创建一个带有标准设置的build.gradle文件,只有在项目目录下没有pom.xml文件时这个task才可用。 |
|generateSettingsFile |创建一个settings.gradle文件,通常用来配置多项目构建。只有在项目目录下没有pom.xml文件时这个task才可用。 |
|maven2Gradle |通过分析项目目录下的POM文件将一个Maven项目转换成Gradle项目(通常作为构建迁移的一部分)。这个task运行完成后,build.gradle和settings.gradle文件就被自动创建了。只有在没有pom.xml文件时这个task才可用。 |
|wrapper |在Gradle项目目录下生产Gradle Wrapper文件,使用与Gradle运行时相同的版本。 |

## 3、常用选项

| 名字 | 描述 |
|--------|--------|
|-?, -h, --help |打印出所有可用的命令行选项,包含描述信息。 |
|-a, --no-rebuild |避免重新构建多项目构建中的所有子项目(也叫作部分构建)。通过使用部分构建,可以节约检查子项目模型的开销,降低构建执行时间。 |
|-b, --build-file |Gradle构建脚本默认的命名约定是build.gradle。使用这个选项执行其他名字的构建脚本(如 gradle -b test.gradle build)。 |
|-c, --settings.file |Gradle设置文件默认的命名约定是settings.gradle。使用这个选项执行非标准设置文件名的构建(比如, gradle -c mySettings.gradle build)。 |
|--continue |在一个task执行失败后Gradle会继续执行。在多项目构建中这个选项极其有用。它让你在构建时发现所有可能的问题,并一起修复它们,而不必一一修复。 |
|--configure-on-demand |这个选项的目的是优化初始化多项目构建的配置时间。这种模式尝试只配置跟正在请求的task相关的项目。这个选项可以通过在gradle.properties文件中设置org.gradle.configure-ondemand属性来激活。 |
|-g, --gradle-user-home |Gradle的默认home目录位于home目录下的.gradle目录中。如果你想要指向不同的目录,则使用这个选项。 |
|--gui |运行一个基于Swing的图形化用户界面。 |
|-I, --init-script |设置一个初始化脚本用于构建。这个脚本会在所有构建task执行前被执行。 |
|-p, --project-dir |默认的,Gradle会在当前目录下执行构建。通过这个选项,你可以指定不同的目录来执行构建。 |
|--parallel |并行构建参与多项目构建的子项目。Gradle会自动确定最优的线程数。这个选项可以通过gradle.properties文件中设置org.gradle.parallel属性来激活。 |
|--parallel-threads |当并行构建多项目构建的时候,这个选项可以被用来重写线程数(比如,--parallel-threads=5)。 |
|-m, --dry-run |打印task的执行顺序,而不必真的执行他们。如果你想要快速的确定task的执行顺序,这个选项会很方便。 |
|--profile |除了每次构建时输出总的构建时间,你可以将构建时间拆分得更小。profile选项在build/reports/profile/目录下生成了详细的HTML报告,其中列出了所有task的执行时间和在配置阶段所用的时间。 |
|--return-tasks |重新运行task执行图中所有确定的task。这个选项会忽略前面task执行的任何UP-TO-DATE状态。 |
|-u, --no-search-upwards |告诉Gradle不要在父目录中寻找设置文件。在有深层次嵌套的项目结构中,这个选项被用来避免在父目录中搜索,从而节约时间。 |
|-v, --version |打印出Gradle运行时的版本信息。 |
|-x, --exclude-task |指定某个task在构建的时候不执行。一个比较典型的例子就是如果你想执行一个完整的构建,但是不执行所有的单元测试(比如,gradle -x test build)。 |

## 4、属性选项

| 名字 | 描述 |
|--------|--------|
|-D, --system-prop |Gradle以JVM进程的形式运行。与所有Java的进程一样,你可以指定系统属性如: -Dmyprop=myvalue。 |
|-P, --project-prop |项目属性是在构建脚本中能够被使用的变量。你可以使用这个选项从命令行直接将一个参数传递到构建脚本中(比如, -Pmyprop=myvalue)。 |

## 5、日志选项

| 名字 | 描述 |
|--------|--------|
|-i, --info |在默认设置下Gradle构建并不会输出大量的日志信息。通过这个选项将日志级别设置成INFO来获得更多的日志信息。 |
|-d, --debug |以DEBUG日志级别运行Gradle构建,将会产生大量的日志信息,包括堆栈跟踪信息,这在差错的时候特别有用。 |
|-q, --quiet |减少构建输出只剩下错误信息。 |
|-s, --stacktrace |如果构建出错了,你会希望知道哪里出错了。如果有异常抛出,这个-s选项会打印出一个简单的堆栈跟踪信息,这个调试失败构建的时候非常有用。 |
|-S, --fullStacktrace |打印出完整的异常堆栈信息。 |

## 6、缓存选项

| 名字 | 描述 |
|--------|--------|
|--offline |通常你的构建定义了一些依赖,如果这些依赖在本地没有存储,并且运行构建的时候没有网络连接就会引起构建失败。使用这个选项,可以让构建采用离线模式运行,并且只检查本地存储的依赖。 |
|--project-cache-dir |默认的依赖缓存目录位于用户目录中的。gradle目录下。这个选项可以被用来指定一个不同的目录。 |
|--recompile-scripts |Gradle默认编译所有的脚本并存储在本地缓存中以提高构建性能。使用这个选项来清空这些缓存。 |
|--refresh-dependencies |手动刷新缓存中的依赖。这个标志强制检查依赖的版本。 |

## 7、后台守护进程选项

| 名字 | 描述 |
|--------|--------|
|--daemon |使用后台守护进程模式执行构建可以提高构建性能。如果后台进程已经存在,则会重用它,如果不存在,则会启动一个新的后台进程。后台守护进程可以通过在gradle.properties文件中设置org.gradle。daemon属性来激活。 |
|--foreground |在终端运行Gradle后台守护进程,用于调试和监控目的。 |
|--no-daemon |不使用已有的Gradle后台守护进程执行构建。 |
|--stop |终止一个已经存在的Gradle后台守护进程。 |