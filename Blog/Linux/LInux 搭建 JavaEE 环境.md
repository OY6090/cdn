# LInux 搭建 JavaEE 环境  

## 一、安装JDK(1.8)

**先将软件通过 xftp5 上传到 /opt 下**  

1. **解压缩到 /opt**  

![image-20200715223356015](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200715223403.png)

2. **配置环境变量的配置文件 vim /etc/profile**  

```
JAVA_HOME=/opt/opt/jdk1.8.0_261
PATH=/opt/jdk1.8.0_261/bin:$PATH
export JAVA_HOME PATH
```

![image-20200715224230019](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200715224230.png)

3. **需要注销用户，环境变量才能生效**

   如果是在 3 运行级别， **logout**

   如果是在 5 的运行级别

   ![image-20200715224455768](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200715224457.png)

4. **在任何目录下就可以使用 java 和 javac**  

   ![image-20200715224552751](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200715224553.png)

5. **测试是否安装成功**  

   编写一个简单的 Hello.java 输出"hello,world!" 

   ```java
   public class Hello{
           public static void main(String[] args){
                   System.out.println("hello");
           }
   }
   ```

   ![image-20200715225622172](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200715225623.png)

   **使用javac 编译  , 在使用java 执行**

   ![image-20200715225659958](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200715225701.png)

## 二、Tomcat 服务器搭建

1. **解压缩到/opt**  

![image-20200715225913184](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200715225915.png)

2**.启动 tomcat ./startup.sh**  

​	先进入到 tomcat 的 bin 目录

​													![image-20200715230312437](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200715230313.png)   

​													![image-20200715230539086](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200715230541.png)	

​	在liunx浏览器中，输入http://localhost:808 启动成功即可。



3. **开放端口 8080 ,这样外网才能访问到 tomcat**  （CentOS7）

   ① **检验防火墙是否启动**

   ​	输入命令 "  ==firewall-cmd --state== " 如果出现如图所示的这种情况说明正在运行，如果没有正在运行需要执行命令" ==systemctl start firewalld== "开启防火墙服务

   ![image-20200716015151199](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200716015152.png)

​	② **配置防火墙，开放8080端口**

```
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --reload
```

4.**开放端口 8080 ,这样外网才能访问到 tomcat**  （CentOS7 以下）

**vim /etc/sysconfig/iptables**  

![image-20200716015604853](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200716015605.png)

**重启防火墙**  

​	![image-20200716015637468](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200716015638.png)

## 三、Tomcat 启动失败解决方案（启动成功跳过）

1. **启动tomcat**

    进入 tomcat 所在的目录的 bin 的文件夹下执行" **./ startup.sh**" 命令 启动 tomcat ，如果出现下面这种情况说明 tomcat 启动 成功。

   ![image-20200716020125408](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200716020126.png)

2.  **验证 tomcat 是否启动成功**

     输入" **ps -ef|grep tomcat** " 命令验证 tomcat 是否启动成功，如果出现下面这种情况说明启动成功。

   ![image-20200716020210587](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200716020211.png)

3.  若启动成功，在linux中输入curl  [http://192.168.112.130:8080](http://192.168.31.128:8080/)（自己linux的ip）看是否正常访问。

   **如下则表示正常访问：**

   ![image-20200716020306410](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200716020307.png)

4. **检验防火墙是否启动**

    输入命令 "  **==firewall-cmd --state==** " 如果出现如图所示的这种情况说明正在运行，如果没有正在运行需要执行命令" **==systemctl start firewalld==** "开启防火墙服务

   ![image-20200716020419634](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200716020420.png)

5. **检查8080端口是否被防火墙开启**

   输入命令" ==**firewall-cmd --permanent --zone=public --list-ports**== “  如果终端输出 “8080/tcp” 则说明8080端口被开启

   如果没有该输出则需要执行命令" ==**firewall-cmd --zone=public --add-port=8080/tcp --permanent**=="开启8080端口, 出现" ==**success**==" 则表示添加成功。

6. **重新启动防火墙**

   输入命令" firewall-cmd --reload" 重新启动防火墙，出现” success“ 字样则表示重新启动成功。

7. **验证开启的8080端口是否生效**

   输入命令” firewall-cmd --zone=public --query-port=8080/tcp“ 验证8080端口是否生效，如果出现 ” yes “字样则代表生效。

   此时，重新启动tomcat就可以使用外部浏览器访问centos 中的tomcat啦。

**补充：**

​	如果以上还没有解决，或者tomcat提示需要配置环境。请去去查看你的**JDK**的配置信息，配置文件在安装JDK中以提及。没有发现问题，可以重启Linux,重新登入。

## 四 、Eclipse 的安装  

1. **解压缩到/opt**    

   ![image-20200716231441236](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716231441236.png)

2. **启动 eclipse**  

   进入到 eclipse 解压后的文件夹， 然后执行 ./eclipse  

## 五、mysql 的安装和配置  

【说明】：因为mysql安装时间较长，所以我已经把安装步骤放到我博客的文件中了。有需要的话。点击链接下载即可。或者你可以百度用yum安装。
