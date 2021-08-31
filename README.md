# elasticsearch-learning
## es 学习笔记
源码搭建步骤
### 1.git clone git@github.com:elastic/elasticsearch.git
### 2.git tag
### 3.git checkout v6.3.2
4.在进行clone 代码之前需要核对当前es 需要的gradle 版本，jdk版本，版本要求比较严格的，对应不上去会出现错误
5.切换到elasticsearch 目录下，执行 ./gradlew idea
6.导入到idea 中，并且更改build tools->gradle 的配置
![image](https://user-images.githubusercontent.com/20039839/131476529-b9bea984-da36-43fc-8c69-6cb051ffe00c.png)
7.配置对应的jdk 等信息
8.找到对应的服务端启动类
![image](https://user-images.githubusercontent.com/20039839/131476735-b813f5c4-85b4-4c4f-adc4-0eb4ffb578fb.png)
9. 在启动之前需要配置四个vm options参数 （elasticsearch-6.3.2 为下载的对应版本的release 版本，主要是使用其中config 服务才能起来）
    1.-Des.path.conf=/xxxx/Documents/elasticsearch-6.3.2/config （未配置会出现[es.path.conf] must not null的错误）
    2.-Des.path.home=//xxxx/Documents/elasticsearch-6.3.2。
    3.-Djava.security.policy=/xxxx/Documents/elasticsearch-6.3.2/home/java.policy （未配置的话，会提示某个类无权限访问,错误截图如下，
       注意：改动点：build.gradle（server/org/elasticsearch/bootstrap/Elasticsearch.java） compileOnly project(':libs:plugin-classloader') 更改为 compile project(':libs:plugin-classloader')，第二，新建一个java.policy 文件，内容为grant {
    permission java.lang.RuntimePermission "createClassLoader";
}; 并且在JAVA_HOME/conf/security/java.policy 文件中的grant 下加入允许：permission java.lang.RuntimePermission "createClassLoader";）
    ![image](https://user-images.githubusercontent.com/20039839/131477233-37ad6302-0716-4c31-8c5d-6f39ce2c6e24.png)
    4.-Dlog4j2.disable.jmx=true
10.至此可以启动起来
11.验证启动成功：1. http://localhost:9200/  2.http://localhost:9200/_cat/health?v
   
    
