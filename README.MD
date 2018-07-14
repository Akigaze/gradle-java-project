## 构建Java项目
> gradle init --type java-application

## 编译Java项目
> gradle build

此时会在项目的`./build/classes`路径下生成项目所有java文件的class文件

## 执行自动化测试
> gradle test

该命令会执行`test`目录下的所有测试文件  
为`test`任务添加显示日志的方法，用`started`标识一个测试的开始，通过的测试显示`passed`,失败的显示`failed`
```groovy
    test {
        testLogging {
            // Show that tests are run in the command-line output
            events 'started', 'passed'
          }
    }
```
>gradle -Dtest.single=**测试的类名** test

指定某个类，进行单独测试
## 添加IDEA插件，生成IDEA项目文件
> apply plugin: 'idea'

在`build.gradle`文件中添加IDEA的插件
同时指定项目的jdk版本，减少手动设置
```groovy
    idea.project {
         jdkName = '1.8'
         languageLevel = '1.8'
    }
```
## 执行程序
> gradle run

执行的主程序配置在`build.gradle`文件的`mainClassName`项目中
> mainClassName = 'App'

## 添加Mockito依赖，在测试方法使用Mockito
从Maven Repository搜索找Mockito的依赖声明，并添加到`build.gradle`中
> testCompile group: 'org.mockito', name: 'mockito-core', version: '2.18.3'

```Java
    LinkedList mockedList = mock(LinkedList.class);
    when(mockedList.get(0)).thenReturn(value);
 ```
使用`mock`方法创建mock对象
使用`when`和`thenReturn`控制mock对象在执行指定方法时的返回值
