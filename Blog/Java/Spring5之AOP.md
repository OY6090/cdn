## 一、AOP（概念）

（1）面向切面编程（方面），利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

（2）通俗的描述：不通修改源代码方式，在主功能里面添加新功能

（3）使用登录例子说明 AOP

**图示：**

![image-20200723000702851](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200723000710.png)

## 二、AOP (底层原理)

### 1、AOP底层使用动态代理

**（1）有两种情况动态代理**

​	**第一种 有接口情况，使用JDK动态代理**

* 创建接口实现类代理对象，增强类的方法

![image-20200723001348703](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200723001349.png)

**第二种没有接口情况，使用CGLIB动态代理**

* 创建子类代理对象，增强类的方法

![image-20200723001640975](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200723001641.png)

## 三、AOP(JDK 动态代理)

### 1、使用JDK 动态代理，使用Proxy 类里面的方法创建代理对象

![image-20200723002154900](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200723002155.png)

**（1）调用 newProxyInstance 方法**

![image-20200723002258467](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200723002259.png)

方法有三个参数：

第一参数：类加载器

第二参数：增强方法所在的类，这个类实现的接口，支持多个接口

第三参数，实现这个接口 InvocationHandler, 创建代理对象，写增强的部分

### 2、编写JDK 动态代理代码

（1）创建接口，定义方法

~~~java
public interface UserDao {
	public int add(int a,int b);
	public String update(String id);
}
~~~

（2）创建接口实现类，实现方法

~~~java
public class UserDaoImpl implements UserDao {
	@Override
	public int add(int a, int b) {
		return a+b;
	}
	@Override
    public String update(String id) {
		return id;
	}
}
~~~

（3）使用 Proxy 类创建接口代理对象

~~~java
public class JDKProxy {
    public static void main(String[] args){
        //创建接口实现类代理对象
        Class[] interfaces = {UserDao.class};
// Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces,new InvocationHandler() {
// 	@Override
// public Object invoke(Object proxy, Method method, Object[] args)throws Throwable {
// 		return null;
// 	}
// });        
        UserDaoImpl userDao = new UserDaoImpl();
        UserDao dao = (UserDao) Proxy.newProxyInstance(JDKProxy.class.getClassLoader(), interfaces, new UserDaoProxy(userDao));
        int result = dao.add(1,2);
        System.out.println("result="+result);
    }
}
// 创建代理对象的代码
class UserDaoProxy implements InvocationHandler{
    // 1.把创建的是谁的代理对象，把谁传递过来
    // 有参数构造传递
    private Object obj;
    public UserDaoProxy(Object obj){
        this.obj = obj;
    }
    // 增强的逻辑
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        // 方法之前
        System.out.println("方法执行...."+method.getName()+":传递的参数..."+ Arrays.toString(args));
        // 被增强的方法执行
        Object res = method.invoke(obj, args);
        // 方法之后
        System.out.println("方法之后执行..."+obj);
        return res;
    }
}
~~~

## 三、AOP 术语

### 1、连接点

​	类里面哪些方法可以被增强，这些方法称为连接点

### 2、切入点

​	实际被真正增强的方法，称之切入点

### 3、通知（增强）

​	（1） 实际增强的逻辑部分称为通知

​	（2）通知的多种类型

​		① 前置通知   ② 后置通知 ③ 环绕通知 ④ 异常通知  ⑤ 最终通知

### 4、切面

​	把通知应用到切入点的过程

## 四、AOP操作

### 1、Spring框架一般都是基于AspectJ实现 AOP 操作

​	AspectJ 不是 Spring 组成部分，独立AOP 框架， 一般把AspectJ 和 Spring 框架一起使用，进行 AOP 操作

### 2、基于AspectJ 实现 AOP 操作

​	（1）基于xml配置文件实现

​	（2）基于注解方式实现（使用）

### 3、在项目工程里面引入AOP 相关依赖

​	![image-20200723112125943](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200723112133.png)

### 	4、切入点表达式

​	（1）切入点表达式作用：知道对哪个类里面的哪个方法进行增强

​	（2）语法结构：execution(\[权限修饰符]\[返回值类型]\[类全路径]\[方法名称][参数列表])

* 举例1: 对com.oy.dao.BookDao 类里面的 add 进行增强

  ~~~java
  execution(* com.oy.dao.BookDao.add(..))
  ~~~

* 举例2：对com.oy.dao.BookDao 类里面的所有的方法进行增强

  ~~~java
  execution(*.com.oy.dao.BookDao.*(..))
  ~~~

* 举例 3：对 com.atguigu.dao 包里面所有类，类里面所有方法进行增强

  ~~~java
  execution(* com.atguigu.dao.*.* (..))
  ~~~

## 五、AOP操作（AspectJ 注解）

### 1、创建类，再类里面定义方法

~~~java
public class User {
    public void add(){
        System.out.println("add....");
    }
}
~~~

### 2、创建增强类（编写增强逻辑）

​	（1）在增强类里面，创建方法，让不同的代表不同的通知类型

~~~java
//增强的类
public class UserProxy {
	public void before() {//前置通知
		System.out.println("before......");
	}
}
~~~

### 3、进行配置的通知

（1）在Spring 配置文件中，开始注解扫描

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                        http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                        http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">
    <!--开启注解扫描-->
    <context:component-scan base-package="com.oy.online.Spring.aopanno"></context:component-scan>
~~~

​	(2) 使用注解创建类 User 和 UserProxy 对象

![image-20200723115951605](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200723115952.png)

​	（3）在增强类上面添加注解 **@Aspect**

~~~java
//增强的类
@Component
@Aspect //生成代理对象
public class UserProxy {
~~~

​	（4）在spring 配置文件中华开启生成代理对象

~~~java
<!-- 开启 Aspect 生成代理对象-->
<aop:aspectj-autoproxy></aop:aspectj-autoproxy>
~~~

### 4、配置不同类型的通知

​	（1）在增强类里面，在作为通知方法上面添加通知类型的注解，使用切入点表达式配置

~~~java
@Component
@Aspect
public class UserProxy {
    // 前置通知
    // @Before 注解表示作为前置通知
    @Before(value = "execution(* com.oy.online.Spring.aopanno.User.add(..))")
    public void before(){// 前置通知
        System.out.println("before....");
    }

    //后置通知（返回通知）
    @AfterReturning(value = "execution(* com.oy.online.Spring.aopanno.User.add(..))")
    public void afterReturning(){// 前置通知
        System.out.println("afterReturning....");
    }

    //最终通知
    @After(value = "execution(* com.oy.online.Spring.aopanno.User.add(..))")
    public void after(){// 前置通知
        System.out.println("after....");
    }

    //异常通知
    @AfterThrowing(value = "execution(* com.oy.online.Spring.aopanno.User.add(..))")
    public void afterThrowing(){
        System.out.println("afterThrowing.........");
    }

    // 环绕通知
    @Around(value = "execution(* com.oy.online.Spring.aopanno.User.add(..))")
    public void around(ProceedingJoinPoint proceedingJoinPoint)throws Throwable{
        System.out.println("环绕之前.........");
        //被增强的方法执行
        proceedingJoinPoint.proceed();
        System.out.println("环绕之后.........");
    }
}    
~~~

### 5、相同的切入点抽取

~~~java
 	// 相同切入点
    @Pointcut(value = "execution(* com.oy.online.Spring.aopanno.User.add(..))")
    public void pointdemo(){
    }
    // 前置通知
    // @Before 注解表示作为前置通知
    @Before(value = "pointdemo()")
    public void before(){// 前置通知
        System.out.println("before....");
    }
~~~

### 6、有多个增强类同一个方法进行增强，设置增强类优先级

​	（1）在增强类上面添加注释 **@Order**（数字类型值），数字类型值越小优先级越高

~~~java
@Component
@Aspect
@Order(1)
public class PersonProxy {
    @Before(value = "execution(* com.oy.online.Spring.aopanno.User.add(..))")
    public void before(){// 前置通知
        System.out.println("PersonProxy before....");
    }
}
~~~

### 7、完全使用注解开发

​	（1）创建配置类，不需要创建xml 配置文件

~~~java
@Configuration
@ComponentScan(basePackages = {"com.oy.online.Spring.aopanno"})
@EnableAspectJAutoProxy(proxyTargetClass = true)
public class ConfigAOP {
}
~~~

测试：

~~~java
@Test
public void test2(){
   ApplicationContext context = new AnnotationConfigApplicationContext(ConfigAOP.class);

   User user = context.getBean("user", User.class);
   user.add();
}
~~~

## 六、AOP操作（AspectJ 配置文件）

### 1、创建两个类，增强类和被增强类，创建方法

~~~java
// 被增强类
public class Book {
    public void buy(){
        System.out.println("add.....");
    }
}
~~~

~~~java
// 增强类
public class BookProxy {
    public void before(){
        System.out.println("before.....");
    }
}
~~~

### 2、在Spring 配置文件中创建两个类的对象

~~~xml
<!--创建对象-->
    <bean id="book" class="com.oy.online.Spring.aopxml.Book"></bean>
    <bean id="bookProxy" class="com.oy.online.Spring.aopxml.BookProxy"></bean>
~~~

### 3、在Spring 配置文件中配置切入点

~~~xml
 <!--配置aop增强-->
    <aop:config>
        <aop:pointcut id="p" expression="execution(* com.oy.online.Spring.aopxml.Book.buy(..))"/>
        <!--配置切面-->
        <aop:aspect ref="bookProxy">
            <!--增强作用在具体的方法上-->
            <aop:before method="before" pointcut-ref="p"></aop:before>
        </aop:aspect>
    </aop:config>
~~~

### 4、测试类

~~~java
    @Test
    public void test3(){
        ApplicationContext context = new ClassPathXmlApplicationContext("bean2.xml");

        Book book = context.getBean("book", Book.class);
        book.buy();
    }
~~~

![image-20200723161840553](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200723161841.png)
