## Spring5 介绍

1. Spring 是轻量级的开源的JavaEE 框架

2. Spring 可以解决企业应用开发的复杂性

3. Spring 有两个核心部分：IOC 和 Aop

   (1) IOC : 控制反转，把创建对象过程给Spring进行管理

   (2) Aop: 面向切面，不修改源代码进行功能增强

4. Spring 特点

   （1）方便解耦，简化开发

   （2）Aop编程支持

   （3）方便程序测试

   （4） 方便和其他框架进行整合

   （5）方便进行事务操作

   （6）降低API 开发难度

## Spring5 入门案例

1. 使用idea创建一个普通的java工程

2. 导入Spring5 相关的jar包（先去Spring官网下载）

   ![image-20200720000532117](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200720000533.png)

![image-20200720000545998](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200720000547.png)

3. 创建普通类，在这个类创建普通方法

~~~java
public class User{
    public void add(){
       System.out.println("add....");
    }
}
~~~

4. 创建Spring配置文件，在配置文件配置创建的对象（bean1.xml）

![image-20200720000855494](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200720000856.png)

~~~java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--配置User对象的创建-->
    <bean id="user" class="com.oy.online.spring.User"></bean>
</beans>
~~~

5.进行测试代码编写

~~~java
@Test
public void userTest(){
    // 1.加载Spring配置文件
    ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");

    // 2.获取配置创建的对象
    User user = context.getBean("user", User.class);
    System.out.println(user);
    user.add();
}
~~~

![image-20200720001341048](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200720001342.png)

## 一、IOC(概念和原理)

### 1、IOC

* 控制反转，把对象创建和对象之间的调用过程，交给Spring进行管理

* 使用IOC目的：为了耦合度降低

### 2、IOC底层原理

* xml 解析、工厂模式、反射

![image-20200720002537623](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200720002538.png)

## 二、 IOC(BeanFactory 接口)

1. IOC思想基于IOC容器完成，IOC容器底层就是对象工厂

2. Spring 提供IOC容器实现的两种方式:（两个接口）

   (1) BeanFactory:  IOC容器基本实现，是Spring内部的使用接口，不提供开发人员进行使用

   ​		**加载配置文件时候不会加载，在获取对象（使用）才会去创建对象**

   (2)ApplicationContext: BeanFactory 接口的子接口，提供更多更强大的功能，一般有开发人员进行使用

   ​		**加载配置文件时候就会把配置文件对象进行创建**

3. ApplicationContext 接口有实现类

![image-20200720003502372](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200720003503.png)

## 三、IOC操作 Bean 管理（概念）

### 1、Bean 管理

1. Bean管理指的是两个操作
2. Spring 创建对象
3. Spring 注入属性

### 2、Bean管理的操作的两种方式

1. 基于xml配置文件方式实现
2. 基于注解方式实现

## 四、IOC操作Bean管理（基于xml方式）

### 1、基于xml方式创建对象

~~~java
<!--配置User对象的创建-->
<bean id="user" class="com.oy.online.spring.User"></bean>
~~~

(1) 在spring 配置文件中，使用bean标签，标签里面添加对应属性，就可以实现对象的创建

(2) 在bean标签有很多属性，介绍常用属性

* Id属性 ： 唯一标识符
* class属性：类全路径（包类路径）

(3)  创建对象时候，默认也是执行无参构造器完成对象的创建

### 2、基于xml方式注入属性

（1）DI：依赖注入，就是注入属性

### 3、第一种注入方式：使用set方法进行注入

​	(1) 创建类，定义属性和对应的set方法

~~~java
public class Book {
    // 创建属性
    private String bname;
    private String bauthor;
    // 创建属性对应的set方法
    public void setBname(String bname){
        this.bname = bname;
    }
    public void setBauthor(String bauthor){
        this.bauthor = bauthor;
    }

    // 测试方法
    public void show(){
        System.out.println(bname+"::"+bauthor);
    }
}
~~~

​	(2) 在spring配置文件配置对象创建，配置属性注入

~~~java
  <!--配置Book对象的创建-->
    <!--set 方法注入属性-->
    <bean id="book" class="com.oy.online.spring.Book">
        <!--使用property 完成属性的注入
            name : 类里面属性名称
            value: 向属性注入的值
        -->
        <property name="bname" value="Java编程之美"></property>
        <property name="bauthor" value="Java"></property>
    </bean>
~~~

### 4、第二种注入方式：使用有参数构成进行注入

​	(1) 创建类，定义属性，创建属性对应有参数构造方法

~~~java
public class Order {
    // 属性
    private String oname;
    private String address;

    // 有参数构造
    public Order(String oname, String address){
        this.oname = oname;
        this.address = address;
    }

    // 测试方法
    public void show(){
        System.out.println(oname+"::"+address);
    }
}
~~~

​	(2) 在spring配置文件中的进行配置

~~~java
 <!--有参构造函数注入属性-->
    <bean id="order" class="com.oy.online.spring.Order">
        <constructor-arg name="oname" value="电脑"></constructor-arg>
        <constructor-arg name="address" value="China"></constructor-arg>
    </bean>
~~~

### 5、p空间名称注入（了解）

​	(1) 使用 p 名称空间注入，可以简化基于 xml 配置方式

第一步 添加p名称空间在配置文件中

**xmlns:p="http://www.springframework.org/schema/p"**

~~~java
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 			   http://www.springframework.org/schema/beans/spring-beans.xsd">
</beans>
~~~

第二步 进行属性注入，在bean标签里面进行操作

~~~
<!--set 方法注入属性-->
<bean id="book" class="com.oy.online.spring.Book" p:bname="java编程之美" p:bauthor="java"></bean>
~~~

## 五、IOC操作Bean 管理（xml注入其他类型属性）

### 1、 字面量

（1）null 值

~~~java
 <property name="address">
   <null/>
</property>
~~~

​	(2) 属性包含特殊符号

~~~java
<!--属性值包含特殊符号
1 把<>进行转义 &lt; &gt;
2 把带特殊符号内容写到 CDATA
-->
<property name="address">
	<value><![CDATA[<<南京>>]]></value>
</property>
~~~

### 2、注入属性-外部bean

(1) 创建两个类service 类 和 dao 类

(2) 在service 调用dao 里面的方法

(3) 在spring 配置文件中进行配置

~~~java
public class UserService {
	//创建 UserDao 类型属性，生成 set 方法
    private UserDao userDao;
    public void setUserDao(UserDao userDao) {
    	this.userDao = userDao;
    }
    public void add() {
    	System.out.println("service add...............");
    	userDao.update();
    }
}
~~~

~~~java
<!--1 service 和 dao 对象创建-->
<bean id="userService" class="com.atguigu.spring5.service.UserService">
    <!--注入 userDao 对象
        name 属性：类里面属性名称
        ref 属性：创建 userDao 对象 bean 标签 id 值
    -->
	<property name="userDao" ref="userDaoImpl"></property>
</bean>
<bean id="userDaoImpl" class="com.atguigu.spring5.dao.UserDaoImpl"></bean>
~~~

### 3、注入属性-内部bean

（1） 一对多关系：部门和员工

​			一个部门有多个员工，一个员工属于一个部门

​			部门是一，员工是多

 （2）在实体类之间表示一对多关系，员工表示所属部门，使用对象类型属性进行表示 

​	部门：

~~~java
public class Dept {
    private String dname;

    public void setDname(String dname) {
        this.dname = dname;
    }

    @Override
    public String toString() {
        return "Dept{" +
                "dname='" + dname + '\'' +
                '}';
    }
}
~~~

​	员工：

~~~java
public class Emp {
    private String ename;
    private String gender;
    // 员工属于某一个部门，使用对象形式表示
    private Dept dept;

    public void setEname(String ename) {
        this.ename = ename;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }

    public void setDept(Dept dept) {
        this.dept = dept;
    }

    public void show(){
        System.out.println(ename + "::" + gender + "::" + dept);
    }
}
~~~

​	(3)  在Spring配置文件中进行配置

~~~java
<!--内部bean-->
    <bean id="emp" class="com.oy.online.spring.bean.Emp">
        <!--设置两个普通属性-->
        <property name="ename" value="jack"></property>
        <property name="gender" value="女"></property>
        <!--设置对象类型属性-->
        <property name="dept">
            <bean id="dept" class="com.oy.online.spring.bean.Dept">
                <property name="dname" value="设计部"></property>
            </bean>
        </property>
    </bean>
~~~

​	测试：

~~~java
 @Test
public void EmpTest(){
    // 加载Spring配置文件
    ApplicationContext context = new ClassPathXmlApplicationContext("bean3.xml");

    // 获取创建对象
    Emp emp = context.getBean("emp", Emp.class);
    System.out.println(emp);
    emp.show();
}
~~~

![image-20200720234512323](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200720234514.png)

### 4、注入属性-级联赋值

1. **第一种写法**

   ~~~xml
   <!--级联赋值-->
   <bean id="emp" class="com.oy.online.spring.bean.Emp">
        <!--设置两个普通属性-->
        <property name="ename" value="lucy"></property>
        <property name="gender" value="女"></property>
        <!--级联赋值-->
        <property name="dept" ref="dept"></property>
   </bean>
   <bean id="dept" class="com.oy.online.spring.bean.Dept">
        <property name="dname" value="技术部"></property>
   </bean>
   ~~~

2. **第二种写法**

   ![image-20200720235820170](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200720235821.png)

   ~~~xml
     <!--级联赋值-->
   <bean id="emp" class="com.oy.online.spring.bean.Emp">
     <!--设置两个普通属性-->
     <property name="ename" value="lucy"></property>
     <property name="gender" value="女"></property>
      <!--级联赋值-->
     <property name="dept" ref="dept"></property>
     <property name="dept.dname" value="财务部"></property>
   </bean>
   <bean id="dept" class="com.oy.online.spring.bean.Dept">
     <property name="dname" value="技术部"></property>
   </bean>
   ~~~

## 六、IOC操作Bean管理（xml注入集合属性）

### 1、注入数组类型属性

### 2、注入List集合类型属性

### 3、注入Map集合属性

（1） 创建类，定义属性、list、map、set类型属性，生成对应的set方法

~~~java
public class Stu {
    // 1.数组类型属性
    private String[] courses;
    // 2. list集合类型属性
    private List<String> list;
    // 3.map 集合类型属性
    private Map<String, String> maps;
    // 4.set集合类型属性
    private Set<String> set;

    public void setCourses(String[] courses) {
        this.courses = courses;
    }

    public void setList(List<String> list) {
        this.list = list;
    }

    public void setMaps(Map<String, String> maps) {
        this.maps = maps;
    }

    public void setSet(Set<String> set) {
        this.set = set;
    }

    @Override
    public String toString() {
        return "Stu{" +
                "courses=" + Arrays.toString(courses) +
                ", list=" + list +
                ", maps=" + maps +
                ", set=" + set +
                '}';
    }
}
~~~

​	（2）在Spring配置文件进行配置

~~~xml
<!--集合类型属性注入-->
    <bean id="stu" class="com.oy.online.Spring.Stu">
        <!--数组类型属性注入-->
        <property name="courses">
            <array>
                <value>java课程</value>
                <value>数据库课程</value>
            </array>
        </property>
        <!--list 类型属性注入-->
        <property name="list">
            <list>
                <value>张三</value>
                <value>李四</value>
            </list>
        </property>
        <!--Map 类型属性注入-->
        <property name="maps">
            <map>
                <entry key="Java" value="java"></entry>
                <entry key="PHP" value="php"></entry>
            </map>
        </property>
        <!--set 类型属性注入-->
        <property name="set">
            <set>
                <value>MySql</value>
                <value>Redis</value>
            </set>
        </property>
    </bean>
~~~

### 4、在集合里面设置对象类型值

​	在Stu中添加属性和方法：

~~~java
	//学生所学多门课程
    private List<Course> courseList;

    public void setCourseList(List<Course> courseList) {
        this.courseList = courseList;
    }
~~~

  在Spring配置文件中

~~~xml
<!--注入 list 集合类型，值是对象-->
<property name="courseList">
   <list>
        <ref bean="course1"></ref>
        <ref bean="course2"></ref>
    </list>
</property>
~~~

~~~xml
<!--创建多个 course 对象-->
<bean id="course1" class="com.oy.online.Spring.Course">
  <property name="cname" value="Spring5框架"></property>
</bean>
<bean id="course2" class="com.oy.online.Spring.Course">
  <property name="cname" value="Mybaits框架"></property>
</bean>
~~~

### 5、把集合注入部分提取出来

（1）在Spring配置文件中引入名称 util

**http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd**

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:util="http://www.springframework.org/schema/util"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd">
~~~

 (2) 使用util标签完成list集合注入提取

~~~xml
	<!--1、提取list集合类型属性注入使用-->
    <util:list id="bookList">
        <value>java编程之美</value>
        <value>java核心卷</value>
        <value>MYSQL必知必会</value>
    </util:list>
    <!--2、提取list集合类型属性注入使用-->
    <bean id="book" class="com.oy.online.Spring.book">
        <property name="list" ref="bookList"></property>
    </bean>
~~~

## 七、IOC操作Bean管理（FactoryBean）

* Spring 有两种类型bean， 一种普通bean, 另外一种工厂bean(FactroyBean)
* 普通bean: 在配置文件中定义bean类型就是返回类型
* 工厂bean：在配置文件定义bean类型可以和返回类型不一样
  * 第一步 创建类，让这个类为工厂bean,实现接口FactoryBean
  * 第二步 实现接口里面的方法，在实现的方法中定义返回的bean类型

~~~java
public class Mybean implements FactoryBean {

    @Override
    public Course getObject() throws Exception {
        Course course = new Course();
        course.setCname("abc");
        return course;
    }

    @Override
    public Class<?> getObjectType() {
        return null;
    }

    @Override
    public boolean isSingleton() {
        return false;
    }
}
~~~

~~~xml
<bean id="myBean" class="com.oy.online.Spring.bean.Mybean"></bean>
~~~

~~~java
 @org.junit.Test
    public void FactoryTest(){
        // 加载Spring配置文件
        ApplicationContext context = new ClassPathXmlApplicationContext("bean2.xml");

        // 获取创建对象
        Course course = context.getBean("myBean", Course.class);
        System.out.println(course);
    }
~~~

## 八、IOC操作Bean管理（bean 作用域）

### 1.在Spring里面，默认情况下，bean是单实例对象

~~~java
@org.junit.Test
public void  BookTest(){
    // 加载Spring配置文件
    ApplicationContext context = new ClassPathXmlApplicationContext("bean2.xml");

    // 获取创建对象
    book book1 = context.getBean("book", book.class);
    book book2 = context.getBean("book", book.class);
    System.out.println(book1);
    System.out.println(book2);
}
~~~

![image-20200721114307906](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200721114750.png)

### 2.设置单实例或多实例

* 在Spring 配置文件bean 标签里面有属性**(scope)**用于设置单实例还是多实例
* scope 属性值
  * 第一个值 默认值，singleton，表示是单实例
  * 第二个值 prototype, 表示第多实例对象

~~~xml
<bean id="book" class="com.oy.online.Spring.book" scope="prototype">
   <property name="list" ref="bookList"></property>
</bean>
~~~

![image-20200721114949659](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200721114951.png)

* singleton 和 prototype 区别

  * 第一 singleton 单实例，prototype 多实例

  * 第二 设置scope 值是 **singleton** 时候，**加载spring配置文件时候就会创建单实例对象**。

    ​		 设置scope 值是 **prototype** 时候，不是加载 spring 配置文件时候创建 对象，**在调用 getBean 方法时候创建多实例对象**。

## 九、IOC操作 Bean 管理（bean 生命周期）

### 1、生命周期

* 从对象创建到对象销毁的过程

### 2、bean 生命周期

* 通过构造器创建bean实例（无参数构造）
* 为bean 的属性设置值 和 对其他bean 引用（调用set方法）
* 调用bean 的初始化的方法（需要进行配置初始化方法）
* bean 可以使用了（对象获取到了）
* 当容器关闭时候，调用bean的销毁方法（需要进行配置销毁的方法）

### 3、演示 bean 生命周期

~~~java
public class Orders {
    private String oname;

    // 无参构造器
    public Orders(){
        System.out.println("第一步 执行无参构造创建 bean 实例");
    }

    public void setOname(String oname) {
        this.oname = oname;
        System.out.println("第二步 调set方法设置属性值");
    }

    // 创建执行的初始化的方法
    public void initMethod(){
        System.out.println("第三步 执行初始化的方法");
    }

    // 创建执行的销毁的方法
    public void destroyMethod(){
        System.out.println("第五步 执行销毁的方法");
    }
}
~~~

~~~xml
<bean id="orders" class="com.oy.online.Spring.bean.Orders" init-method="initMethod"  destroy-method="destroyMethod">
   <property name="oname" value="手机"></property>
</bean>
~~~

~~~java
    @org.junit.Test
    public void OrdersTest(){
//        ApplicationContext context = new ClassPathXmlApplicationContext("bean3.xml");
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("bean3.xml");
        
        Orders orders = context.getBean("orders", Orders.class);
        System.out.println("第四步 获取创建Bean 实例对象");
        System.out.println(orders);
        // 手动让bean实例销毁
        context.close();
    }
~~~

![image-20200721122143974](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200721122144.png)

### 4、bean的后置处理器，bean生命周期

* 通过构造器创建bean实例（无参构造器）
* 为bean的属性设置值和其他bean引用（调用set方法）
* **把bean的实例传递bean后置处理器的方法 **postProcessBefoInitialization
* 调用bean的初始化的方法
* **把bean实例传递bean后置处理器的方法** postProcessAfterInitialization
* bean可以使用（对象获取到了）
* 当前容器关闭时，调用bean的销毁方法（需要精心配制销毁的方法）

### 5、添加后置处理器

~~~java
public class MybeanPost implements BeanPostProcessor {
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("在初始化之前执行的方法");
        return bean;
    }

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("在初始化之后执行的方法");
        return bean;
    }
}
~~~

~~~xml
<!--配置后置处理器-->
<bean id="myBeanPost" class="com.oy.online.Spring.bean.MybeanPost"></bean>
~~~

![image-20200721154557604](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200721154558.png)

## 十、IOC操作Bean管理（XML自动装配）

### 1、自动装配

* 根据指定装配规则（属性名称或者属性类型），Spring自动将匹配的属性值进行注入

### 2、自动装配过程

**（1）根据属性名称自动注入**

~~~java
public class Emp {
    private Dept dept;

    public void setDept(Dept dept) {
        this.dept = dept;
    }

    @Override
    public String toString() {
        return "Emp{" +
                "dept=" + dept +
                '}';
    }
    public void test(){
        System.out.println(dept);
    }
}
~~~

~~~java
public class Dept {
    @Override
    public String toString() {
        return "Dept{}";
    }
}
~~~

~~~xml
    <!--实现自动装配
        bean标签属性autowire,配置自动装配
        autowire 属性常用两个值：
            byName 根据属性名称注入，注入值bean的id值和类型性名称一样
            byType 根据属性类型注入
    -->
    <bean id="emp" class="com.oy.online.Spring.autowire.Emp" autowire="byName"></bean>

    <bean id="dept" class="com.oy.online.Spring.autowire.Dept"></bean>
~~~

**(2) 根据属性类型自动注入**

~~~xml
    <!--实现自动装配
        bean标签属性autowire,配置自动装配
        autowire 属性常用两个值：
            byName 根据属性名称注入，注入值bean的id值和类型性名称一样
            byType 根据属性类型注入
    -->
    <bean id="emp" class="com.oy.online.Spring.autowire.Emp" autowire="byType"></bean>

    <bean id="dept" class="com.oy.online.Spring.autowire.Dept"></bean>
~~~

## 十一、IOC操作 Bean 管理（外部属性文件）

1. **直接配置数据库信息**

   （1）配置德鲁伊连接池

   （2）引入德鲁伊连接池依赖jar包

   ![image-20200722111348312](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200722111356.png)

   ~~~xml
       <!--直接配置连接池-->
       <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
           <property name="driver" value="com.mysql.jdbc.Driver"></property>
           <property name="url" value="jdbc:mysql://localhost:8080/test"></property>
           <property name="username" value="root"></property>
           <property name="password" value="root"></property>
       </bean>
   ~~~

   2. **引入外部属性文件配置数据库连接池**

      (1) 创建外部属性文件，properties 格式文件，写数据库信息

   ~~~properties
   prop.driverClass=com.mysql.jdbc.Driver
   prop.url=jdbc:mysql://localhost:8080/test
   prop.username=root
   prop.password=root
   ~~~

   ​		(2) 把外部 properties 属性文件引入到spring配置文件中

   * 引入context名称空间
     * xmlns:context="http://www.springframework.org/schema/context"
     * http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd

   ~~~xml
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                              http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
   ~~~

   * 在spring配置文件使用标签引入外部属性文件

   ~~~xml
   <!--引入外部属性文件-->
       <context:property-placeholder location="classpath:jdbc.properties"/>
   
       <!--配置连接池-->
       <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
           <property name="driverClassName" value="${prop.driverClass}"></property>
           <property name="url" value="${prop.url}"></property>
           <property name="username" value="${prop.username}"></property>
           <property name="password" value="${prop.password}"></property>
       </bean>
   ~~~

## 十二、IOC操作 Bean管理（基于注解方式）

### 1、注解

​	（1）注解是代码的特殊标记，格式：@注解名称(属性名称=属性值，属性名称=属性值...)

​	（2）使用注解，注解作用在类上面，方法上面，属性上面

​	（3）使用注解目的：简化xml 配置

### 2、Spring 针对Bean 管理中创建对象提供注解

​	（1）@Component

​	（2）@Service

​	（3）@Controller

​	（4）@Repository

**上面四个注解功能是一样的，都可以用来创建bean实例**

### 3、基于注解方式实现对象创建

**第一步 引入依赖**

![image-20200722115433412](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200722115434.png)

**第二步：开始组件扫描**

~~~xml
	<!--开启组件扫描
        1.如果扫描多个包，多个包使用逗号隔开
        2.扫描包上的目录
    -->
    <context:component-scan base-package="com.oy.online.Spring"></context:component-scan>
~~~

**第三步 创建类，在类上面添加创建对象的注解**

~~~java
//在注解里面 value 属性值可以省略不写，
//默认值是类名称，首字母小写
//UserService -- userService
@Component(value = "userService") //<bean id="userService" class=".."/>
public class UserService {
	public void add() {
		System.out.println("service add.......");
	}
}
~~~

### 4、开启组件扫描细节设置

~~~xml
<!--示例 1
	use-default-filters="false" 表示现在不使用默认 filter，自己配置 filter
	context:include-filter ，设置扫描哪些内容
-->
<context:component-scan base-package="com.oy.online.Spring" use-defaultfilters="false">
	<context:include-filter type="annotation"expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
~~~

~~~xml
<!--示例 2
	下面配置扫描包所有内容
	context:exclude-filter： 设置哪些内容不进行扫描
-->
<context:component-scan base-package="com.oy.online.Spring">
	<context:exclude-filter type="annotation"expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
~~~

### 5、基于注解方式实现属性注入

（1）**@Autowired**: 根据属性类型进行自动装配

​	第一步：把 service 和 dao 对象创建，在service 和 dao 类创建对象注解

​	第二步：把 service 注入 dao 对象， 在 service 类添加 dao  类型属性，在属性上面使用注解

~~~java
public interface UserDao {
    public void add();
}
~~~

~~~java
@Repository
public class UserDaoImpl implements UserDao{
    @Override
    public void add() {
        System.out.println("dao add...");
    }
}
~~~

~~~java
@Service
public class UserService {
    // 定义dao 类型属性
    // 不需要添加 set 方法
    // 添加注入属性注解
    @Autowired
    private UserDao userDao;

    public void add(){
        System.out.println("service add....");
        userDao.add();
    }
}
~~~

**测试：**

~~~java
	@Test
    public void test(){
        ApplicationContext context = new ClassPathXmlApplicationContext("bean6.xml");

        UserService userService = context.getBean("userService", UserService.class);
        System.out.println(userService);
        userService.add();
    }
~~~

（2）**@Qualifier**：根据名称进行注入

这个@Qualifier 注解的使用 ，和上面@Autowired 一起使用

~~~java
//定义 dao 类型属性
//不需要添加 set 方法
//添加注入属性注解
@Autowired //根据类型进行注入
@Qualifier(value = "userDaoImpl1") //根据名称进行注入
private UserDao userDao;
~~~

（3）**@Resource**:  可以根据类型注入，可以根据名称注入

~~~java
//@Resource //根据类型进行注入
@Resource(name = "userDaoImpl1") //根据名称进行注入
private UserDao userDao;
~~~

（4）**@Value**：注入普通类型的属性

~~~java
@Value(value = "abc")
private String name;
~~~

### 6、完全注解开发

（1）创建配置类，替代xml配置文件

~~~java
@Configuration // 作为配置类，替代xml 配置文件
@ComponentScan(basePackages = {"com.oy.online.Spring"})
public class SpringConfig {
}
~~~

（2）测试类

~~~java
	@Test
    public void SpringConfigTest(){
        // 加载配置类
        ApplicationContext context = new AnnotationConfigApplicationContext(SpringConfig.class);

        UserService userService = context.getBean("userService", UserService.class);
        System.out.println(userService);
        userService.add();
    }
~~~

