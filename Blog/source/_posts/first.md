1.项目打包运行

* 直接点击package就可以生成jar包

* 可以通过使用```java -jar test.jar``` 的命令来对生成的jar包进行运行



2.springboot的配置

* 启动图片可以在```src/main/resources```目录下的banner文件进行替换更改（最终显示的就是  banner中的内容）这个文件可以是图片也可以是文本。



3.application.yml 为配置文件   

* 配置文件可以用来进行属性的配置    

  ```
  my.blog.name=jarninlee's blog
  my.blog.title=Spring Boot
  ```

  其中@Value("${属性名}")  就可以将配置文件中的值进行注入

  ```
  @Component
  public class BlogProperties {
  	
      @Value("${my.blog.name}")
      private String name;
      
      @Value("${my.blog.title}")
      private String title;
      
      // get,set略	
  }
  ```

由于上面已经被注册为Compent组件，所以可以直接进行该类的实例注入

在属性很多的情况下，还可以使用另一种方式，直接指定一个配置文件中的参数然后自动按照变量名进行填充

```
@ConfigurationProperties(prefix="my.blog")
public class ConfigBean {
    private String name;
    private String title;
    // get,set略
}
```

**需要注意的是使用这种方式，有两种情况：**

​				-直接在Bean类上面添加```@Component```直接将其注册为bean组件

​				-或者在SpringBoot启动类上面添加```@EnableConfigurationProperties( {ConfigBean.class} )```

**这两种都可将ConfigBean注册为Bean类型组件**