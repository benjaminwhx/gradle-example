# Maven的Provided scope的实现
The implementation of provided scope like maven in gradle project

```
configurations {
    provided
}
sourceSets {
    main.compileClasspath += configurations.provided
    test.compileClasspath += configurations.provided
    test.runtimeClasspath += configurations.provided
}
```

这样我们就可以在dependencies中使用provided了,详情请看[]()

我们也可以在使用了war插件的地方直接使用providedCompile,效果和provided一样,详情请看[]()