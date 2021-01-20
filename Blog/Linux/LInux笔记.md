# 第一章 开机、重启和用户登录注销

## Linux 目录结构：

![image-20200707133023667](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707133025.png)

## 1.1 关机&重启命令

* **shutdown**
* shutdown -h now : 表示立即关机
  
* shutdown -h 1 :  表示 1 分钟后关机
  
* shutdown -r now : 立即重启
  
* **halt**

  * 就是直接使用，效果等价于关机

* **reboot**

  * 就是重启系统

* **syn**

  * 把内存的数据同步到磁盘

## 1.2 用户基本登入和注销

### 		1.2.1 基本介绍

​		1）登入时尽量少用root登录，因为它是系统管理员，最大权限，避免操作失误。可利用普通用户登录，登入后再用**"su -用户名"**  命令来切换成系统管理员身份.

​		2)  在提示符输入 **logout** 即可以注销用户

![1594015025921](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706164120.png)

# 第二章 用户管理

## 2.1 添加用户

### 		2.1.1 基本语法

​			**useradd**  [选项]  用户名

### 		2.1.2 实际案例

​		 	添加一个用户 xm

​				![1594015058626](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706164126.png)

​			**特别说明**

​			 **cd** 表示 *change directory*

### 		2.1.3 细节说明

​		 1）当创建用户成功后，会自动的创建和用户名同名的家的目录

​		 2） 也可以通过 **useradd - d**  指定目录 新的用户名，给新创建的用户指定家目录

 ![image-20200716230457171](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716230457171.png)

## 2.2 给用户指定或修改密码

### 		2.2.1基本语法

​			**passwd**  用户名

### 		2.2.2 应用案例

​		1） 给 xm 指定密码

​		![1594015092082](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706164139.png)

## 2.3 删除用户

### 		2.3.1 基本语法

​			**userdel**  用户名

### 		2.3.2 应用案例

​			1）删除用户 xm, 但是要保留加目录

​				![1594015234066](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706164148.png)

​		2）删除用户 xq 以及用户主目录

​				![1594015246507](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706164151.png)

## 2.4 查询用户信息

### 		2.4.1 基本语法

​			**id**  用户名

### 		2.4.2 应用实例

​			**案例1：请查询root 信息**

​			![1594015149857](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706164155.png)

### 	2.4.3 细节说明

​			1）当用户不存在时，返回“无此用户”

## 2.5 切换用户

### 		2.5.1 介绍

​			在操作Linux中，如果当前用户的权限不够，可以通过 **su -** 指令，切换到高权限用户，比如 root。

### 	2.5.2 基本语法

​			**su -**  切换用户名

### 2.5.3 应用实例

​			1) 创建一个用户 zf, 指定密码，然后切换到zf

​			![image-20200706175315058](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706175509.png)

### 2.5.4 细节说明

​		1）从权限高的用户切换到权限低的用户，不需要输入密码，反之需要

​		2）当需要返回到原来的用户时，使用**exit**命名

## 2.6 用户组

###  2.6.1 介绍

​		类似于角色， 系统可以对有共性的多个用户进行统一的管理。  

### 2.6.2 增加组

 		**groupadd** 组名

### 2.6.3 案例演示

​		![image-20200706231729007](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706231853.png)

### 2.6.4 删除组

​		指令（基本语法）

 		**groupdel** 组名

### 2.6.5 案例演示

​		![image-20200706232508125](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706232509.png)

## 2.7 增加用户时直接加上组  

### 2.7.1 指令（基本语法）

​		**useradd -g**  用户组 用户名

### 2.7.2 案例演示

​		**增加一个用户 zwj, 直接将他指定到 wudang**

​			![image-20200706233014550](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706233015.png)

## 2.8 修改用户的组

### 2.8.1 指令（基本语法）

​		**usermod -g**  用户组 用户名

### 2.8.2 案例演示

​		**创建一个 shaolin 组， 让将 zwj 用户修改到 shaolin**



![image-20200706234025775](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706234027.png)

## 2.9 /etc/passwd 文件  

​		用户(user) 的配置文件，记录用户的各种信息

​		每行的含义：用户名：口令：用户标识符：组标识号：注释性描述：主目录：登录 Shell

* **操作代码**

​		![image-20200706235052380](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706235055.png)

![image-20200706234730569](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706234731.png)

## 2.10  /etc/shadow 文件  

​		口令的配置文件

​		每行的含义： 登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动 时间:失效时间:标志  	

## 2.11 /etc/group 文件  

​		组(group)的配置文件 ，记录Linux包含的组的信息

​		每行含义：组名:口令:组标识号:组内用户列表  	

​		![image-20200706235934624](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200706235936.png)

# 第三章 实用指令

## 3.1 指定运行的级别

### 3.1.1运行级别说明：

* 0 ： 关机

* 1 ： 单用户【找回丢失密码】

* 2： 多用户状态没有网络服务

* 3： 多用户状态有网络服务

* 4： 系统未使用保留给用户

* 5： 图形界面

* 6： 系统重启  		

  **常用运行级别是 3 和 5 ， 要修改默认的运行级别可改文件**  

  **/etc/inittab 的 id:5:initdefault:这一行中的数字**

### 3.1.2运行级别的示意图：  

​		

![image-20200707000644701](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707000645.png)

## 3.2 切换到指定运行级别的指令

### 3.2.1 基本语法

​	**init [0123456]**

​		![image-20200707004348669](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707004351.png)

**补充：**

​	关于root密码忘记，改怎么用运行级别的指令来操作，每个版本不同，所以自行百度。

## 3.3 帮助指令

### 3.3.1 介绍

​		当我们对某个指令不熟悉时， 我们可以使用 Linux 提供的帮助指令来了解这个指令的使用方法。 

###  3.3.2 man 获取帮助信息

* **基本语法**

   **man** [命令或配置文件] （功能描述:  获取帮助信息）

* **实用案例**

  ​	**案例：查看ls 命令的帮助信息**

  ​	![image-20200707130907570](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707130915.png)

### 3.3.3 help 指令

* **基本语法**

  ​	**help** 命令 （功能描述： 获取shell 内置命令的帮助信息）

* **应用案例**

  ​	**案例： 查看 cd 命令的帮助信息**

  ​	![image-20200707131312298](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707131313.png)

## 3.4 文件目录类

### 3.4.1 pwd 指令

* **基本用法**

  ​	**pwd** (功能描述： 显示当前工作目录的绝对路径)

* **应用实例**

  ​    **案例：显示当前工作目录的绝对路径**

![image-20200707131633657](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707131634.png)

### 3.4.2 ls 指令

* **基本语法**

  ​	**ls** [选项]  [目录或是文件]

* **应用案例**

  ​	**-a** :   显示当前目录所在的文件和目录，包括隐藏的。

  ​	**-l**  :   以列表的方式显示信息

* **应用实例**

  ​	**案例： 查看当前目录的所在的内容信息**

  ​	![image-20200707132226091](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707132228.png)

  ![image-20200707132349650](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707132351.png)

### 3.4.3 cd 指令

* **基本语法**

  ​	**cd** [参数] （功能切换到指定目录）

* **常用参数**

  ​	==绝对路径== 和 ==相对路径==

  ​	![image-20200707132840549](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707132841.png)

  ​	**cd ~** 	或者 **cd**  : 回到自己的家目录

  ​	**cd..**    回到当前目录的上一级目录	

* **应用实例**

  ​	**案例 1： 使用绝对路径切换到 root 目录** 

  ​	![image-20200707133439217](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707133440.png)

  **案例 2： 回到家目录**  

![image-20200707133554976](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707133556.png)

### 3.4.4 mkdir 指令

​		**mkdir** 指令用于创建目录（make directory）

* **基本用法**

  ​	**mkdir** [选项] 要创建的目录

* **常用选项**

  ​	**-p**  :  创建多级目录

* **应用实例**

  ​	**案例 1:创建一个目录 /home/dog**  

  ​	![image-20200707134540622](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707134541.png)

  ​	**案例 2:创建多级目录 /home/animal/tiger**  

  ![image-20200707134814642](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707134815.png)

### 3.4.5 rmdir 指令

* **介绍**

  ​	**rmdir** 指令删除空目录

* **基本语法**

  ​	**rmdir** [选项]  要删除的空目录

* **应用实例**

  ​	**案例 1:删除一个目录 /home/dog**  

  ​	![image-20200707231324290](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707231403.png)

* **使用细节**

  ​	rmdir 删除的是空目录， 如果目录下有内容时无法删除的。
  ​	提示： 如果需要删除非空目录， 需要使用 rm -rf 要删除的目录  

![image-20200707231655692](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707231657.png)

### 3.4.6 touch 指令

​		**touch** 指令创建空文件

* **基本用法**

  ​	**touch** 文件名称

* **应用实例**

  ​	**案例 1: 创建一个空文件 hello.txt**  

  ​	![image-20200707232140225](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707232141.png)

  ![image-20200707232157579](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707232158.png)

### 3.4.7  cp 指令

​		**cp** 指令拷贝文件到指定的目录

* **基本用法**

  ​	**cp** [选项] source dest

* **常用选项**

  ​	**-r** :  递归复制整个文件夹

* **应用实例**

  ​	**案例 1: 将 /home/aaa.txt 拷贝到 /home/bbb 目录下[拷贝单个文件]**  

  ![image-20200707232812514](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707232813.png)

  **案例 2: 递归复制整个文件夹， 举例 ：将/home/test 整个目录拷贝到 /home/zwj 目录**  

  ![image-20200707233029699](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707233030.png)

* **使用细节**

  ​	强制覆盖不提示的方法： **\cp**

  ​	![image-20200707233351210](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707233352.png)

### 3.4.8 rm 指令

​		rm 指令移除【删除】 文件或目录  

* **基本用法**

  ​	**rm** [选项] 要删除的文件或目录

* **常用选项**

  ​	**-r** :  递归删除整个文件夹

  ​	**-f**  :  强制删除不提示 

* **应用实例**

  ​	**案例 1: 将 /home/aaa.txt 删除**  

  ​	![image-20200707233831071](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707233832.png)

  **案例 2: 递归删除整个文件夹 /home/bbb**  

  ![image-20200707234025761](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707234026.png)

* **使用细节**

  ​	**强制删除不提示的方法： 带上 -f 参数即可**  

  ​	![image-20200707234213136](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707234214.png)

### 3.4.9 cat 指令

​		cat 查看文件内容， 是以只读的方式打开。  

* **基本语法**

  **cat**  [选项]  要查看的文件

* **常用选项**

  **-n** :  显示行号

* **应用实例**

  ​	**案例 1: /etc/profile 文件内容， 并显示行号**  

  ​	

  ![image-20200707235035822](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707235037.png)

* **使用细节**

  ​	cat 只能修改文件， 而不能修改文件，为了浏览方便，一般会带上 管道命令 | more

  ​	cat 文件名 | more [分页浏览]

### 3.4.10 mv指令

​		mv 移动文件与目录或重命名  

* **基本用法**

  ​	**mv** oldNameFile newNameFile (功能描述： 重命名)
  ​    **mv** /temp/movefile /targetFolder (功能描述： 移动文件)  

* **应用实例**

  ​	**案例 1: 将 /home/aaa.txt 文件 重新命名为 pig.txt**

  ​	![image-20200708002334471](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200708002335.png)  

  **案例 2:将 /home/pig.txt 文件 移动到 /root 目录下**  

  ![image-20200708002538638](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200708002539.png)

### 3.4.11 more 指令

​		more 指令是一个基于 VI 编辑器的文本过滤器， ==它以全屏幕的方式按页显示文本文件的内容==。more 指令中内置了若干快捷键， 详见操作说明  

* **基本语法**

  ​	**more** 要查看的文件

* **应用实例**

  ​	**案例: 采用 more 查看文件 /etc/profile**  
  ​	![image-20200707235640390](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707235641.png)

  * **快捷键**

     ![image-20200707235726391](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200707235727.png)

### 3.4.12 less 指令  

​		less 指令用来==分屏查看文件内容==， 它的功能与 more 指令类似， 但是比 more 指令更加强大， 支持各种显示终端。 less 指令在显示文件内容时， 并不是一次将整个文件加载之后才显示， 而是根据显示需要加载内容， 对于显示大型文件具有较高的效率。

* **基本语法**

  ​	**less** 要查看的文件

* **应用实例**

  **案例: 采用 less 查看一个大文件文件 /opt/金庸-射雕英雄传 txt 精校版.txt**  	

  ![image-20200708000045325](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200708000046.png)

  * **快捷键**

    ![image-20200708000115738](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200708000116.png)

### 3.4.13 \> 指令 和 >> 指令  

* **介绍**

  ==\> 指令 和 >> 指令==

  \> 输出重定向 : 会将原来的文件的内容覆盖    	

  \>> 追加： 不会覆盖原来文件的内容， 而是追加到文件的尾部。  

* **基本语法**

  **1) ls -l >文件 （功能描述： 列表的内容写入文件 a.txt 中（==覆盖写==） ）**  	

  ![image-20200708000602451](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200708000603.png)

  说明： ls -l > a.txt , 将 ls -l 的显示的内容覆盖写入到 a.txt 文件， 如果该文件不存在， 就创建该文
  件。

  ​	**2) ls -al >>文件 （功能描述： 列表的内容追加到文件 a.txt 的末尾）**    

  ​	![image-20200708001011568](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200708001012.png)

  **3) cat 文件 1 > 文件 2 （功能描述： 将文件 1 的内容覆盖到文件 2）**

    ![image-20200708001148886](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200708001150.png)

* **应用实例**

  ​	**案例 1: 将 /home 目录下的文件列表 写入到 /home/info.txt 中**  

  ​	![image-20200708001403097](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200708001404.png)

  **案例 2: 将当前日历信息 追加到 /home/mycal 文件中 [提示 cal ]**  

  ​	![image-20200708001737150](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200708001738.png)

### 3.4.14 echo 指令  

​		echo 输出内容到控制台。  

* **基本语法**

  **echo** [选项] [输出内容]  

* **应用实例**

  **案例: 使用 echo 指令输出环境变量,输出当前的环境路径。**  

  ![image-20200708002843661](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200708002844.png)

### 3.4.15 head 指令  

​		head 用于显示文件的开头部分内容， 默认情况下 head 指令显示文件的前 10 行内容  

* **基本语法**

  **head**  文件 (功能描述： 查看文件头 10 行内容)
  **head -n** 5 文件 (功能描述： 查看文件头 5 行内容， 5 可以是任意行数)

* **应用实例**

  **案例: 查看/etc/profile 的前面 5 行代码**  

  ![image-20200708003232118](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200708003233.png)

### 3.4.16 tail 指令

​		 tail 用于输出文件中尾部的内容， 默认情况下 tail 指令显示文件的后 10 行内容。  

* **基本语法**

  1) **tail** 文件 （功能描述： 查看文件后 10 行内容）
  2) **tail -n** 5 文件 （功能描述： 查看文件后 5 行内容， 5 可以是任意行数）
  3) **tail -f** 文件 （功能描述： 实时追踪该文档的所有更新， 工作经常使用）	

* **应用实例**

  **案例 1: 查看/etc/profile 最后 5 行的代码**  	

  ![image-20200708003648317](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200708003649.png)

  **案例 2: 实时监控 mydate.txt , 看看到文件有变化时， 是否看到， 实时的追加日期**  

  ![image-20200708004029822](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200708004030.png)

### 3.4.17 ln 指令

软链接也叫符号链接，类似于window 里的快捷方式，主要存放了链接其他文件的路径。

* **基本用法**

  **In -s**  **[原文件或目录][软连接**] （功能描述：给原文件创建一个软链接）

* **应用实例**

  **案例 1: 在/home 目录下创建一个软连接 linkToRoot， 连接到 /root 目录**  

  ![image-20200713232805422](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200713232806.png)

  **案例 2: 删除软连接 linkToRoot**  

  ![image-20200713233202221](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200713233203.png)

* **细节说明**

  当我们使用pwd指令查看目录时，仍然看到的是软链接所在的目录

### 3.4.18 history 指令

​	查看已经执行的历史命令，也可以执行历史的指令

* **基本用法**

  **history**	(功能描述：查看已经执行的历史命令)

* **应用实例**

  **案例 1: 显示所有的历史命令**  

  ![image-20200713233731397](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200713233732.png)

**案例 2: 显示最近使用过的 10 个指令。**  

![image-20200713233835634](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200713233836.png)

**案例 3： 执行历史编号为 5 的指令**  

![image-20200713234044022](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200713234045.png)

## 3.5 时间日期类

### 3.5.1 date 指令-显示当前日期

* **基本用法**

  1）date	 (功能描述： 显示当前时间)

  2）date+%Y	（功能描述：显示当前年份）

  3）date +%m 	(功能描述： 显示当前月份)

  4）date + %d	(功能描述：显示当前是哪一天)

  5）date"+Y-%m-%d%H:%M:%S" 	(功能描述： 显示年月份时分秒)

* **应用实例**

  **案例 1: 显示当前时间信息**

  ![image-20200713234743533](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200713234744.png)

  **案例 2: 显示当前时间年月日**  

  ![image-20200713234928229](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200713234930.png)

  **案例 3: 显示当前时间年月日时分秒**  

​					![image-20200713235052867](C:\Users\hp\AppData\Roaming\Typora\typora-user-images\image-20200713235052867.png)

### 3.5.2 date 指令- 设置日期

* **基本语法**

  **date**  -s   字符串时间

* **应用实例**

  **案例 1: 设置系统当前时间 ， 比如设置成 2020-10-10 11:22:22**  

  ![image-20200713235354189](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200713235418.png)

### 3.5.3 cal 指令

​	查看日历的指令

* **基本指令**

  cal [选项]	（功能描述）

* **应用实例**

  **案例 1: 显示当前日历**  

![image-20200713235702451](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200713235703.png)

​	**案例 2: 显示 2020 年日历** 

​	 ![image-20200713235753909](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200713235754.png)

## 3.6 搜索查找类

### 3.6.1 find 指令

​	find 指令将从指定目录向下递归地遍历其各个子目录， 将满足条件的文件或者目录显示在终端。  

* **基本用法**

  **find**	[搜索范围]	[选项]

* **选项说明**

  ![image-20200714000105464](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714000106.png)

* **应用实例**

  **案例 1: 按文件名： 根据名称查找/home 目录下的 hello.txt 文件**  

  ![image-20200714000424458](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714000425.png)

  **案例 2： 按拥有者： 查找/opt 目录下， 用户名称为 nobody 的文件**  

  ​	![image-20200714001128962](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714001129.png)

  **案例 3： 查找整个 linux 系统下大于 20m 的文件（+n 大于 -n 小于 n 等于）**  

  ![image-20200714001654034](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714001654.png)

  ​										![image-20200714001802697](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714001804.png)

  ​									![image-20200714001852987](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714001854.png)

**查询 / 目录下， 所有 .txt 的文件**  

![image-20200714002023155](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714002024.png)

### 3.6.2 Locate 指令

​		locaate 指令可以快速定位文件路径。 locate 指令利用事先建立的系统中所有文件名称及路径的ocate 数据库实现快速定位给定的文件。 Locate 指令无需遍历整个文件系统， 查询速度较快。 为了保证查询结果的准确度， 管理员必须定期更新 locate 时刻。

* **基本语法**

  **locate** 	搜索文件

* **特别说明**

  由于 locate 指令基于数据库进行查询， ==所以第一次运行前， 必须使用 updatedb 指令创建 locate 数据库。==  

* **应用案例**

  **案例 1: 请使用 locate 指令快速定位 hello.txt 文件所在目录**  

  ![image-20200714002532343](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714002533.png)

### 3.6.3 grep 指令 和 管道符号

​	grep 过滤查找 ， 管道符， “|”， 表示将前一个命令的处理结果输出传递给后面的命令处理。

*  **基本用法**

  **grep** [选项]  查找内容

* **常用选项**

  ![image-20200714002837504](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714002838.png)

* **应用实例**

  **案例 1: 请在 hello.txt 文件中， 查找 "yes" 所在行， 并且显示行号**  

  ![image-20200714003725265](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714003727.png)

  ![image-20200714003917407](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714003919.png)

## 3.7  压缩和解压类

### 3.7.1 gzip/gunzip 指令

​	gzip 用于压缩文件，gunzip用于解压

* **基本用法**

  **gzip** 	文件	（功能描述）

  **gunzip**	文件	（功能描述：解压文件命令）

* **应用实例**

  **案例 1: gzip 压缩， 将 /home 下的 hello.txt 文件进行压缩**  

  ![image-20200714102151644](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714102152.png)

  **案例 2: gunzip 压缩， 将 /home 下的 hello.txt.gz 文件进行解压缩**  

![image-20200714102332900](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714102335.png)

* **细节说明**

  当我们使用gzip 对文件进行压缩后，捕获保留原来的文件

### 3.7.2 zip/unzip 指令

​	zip 用于压缩文件，unzip用于解压的，这个在项目打包发布中很有用的

* **基本用法**

  **zip**	[选项]XXX.zip 	 将要压缩地内容（功能描述：压缩文件和目录的命令）

  **unzip**	[选项] XXX.zip	（功能描述：解压缩文件）

* **常用选项**

  **-r**	递归压缩，即压缩目录

* **unzip 的常用选项**

  **-d**<目录>：	指定解压后文件的存放目录

* **应用实例**

  **案例 1: 将 /home 下的 所有文件进行压缩成 mypackage.zip**  

  ![image-20200714104318947](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714104319.png)

  ![image-20200714104352860](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714104354.png)

  **案例 2: 将 mypackge.zip 解压到 /opt/tmp 目录下**  

  ![image-20200714104627948](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714104629.png)

### 3.7.3 tar 指令

​	tar **指令 是打包指令** ，最后打包的文件是**.tar.gz** 的文件

* **基本语法**

  tar [选项]	XXX.tar.gz	打包的内容	（功能描述：打包目录,压缩后的文件格式.tar.gz）

* **选项说明**

  ![image-20200714105010507](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714105011.png)

* **应用实例**

  **案例 1: 压缩多个文件， 将 /home/a1.txt 和 /home/a2.txt 压缩成 a.tar.gz**  

  ![image-20200714105757307](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714105758.png)

  **案例 2: 将/home 的文件夹 压缩成 myhome.tar.gz**  

  ![image-20200714105858523](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714105859.png)

  **案例 3: 将 a.tar.gz 解压到当前目录**  

  ![image-20200714110051115](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714110053.png)

  **案例 4: 将 myhome.tar.gz 解压到 /opt/ 目录下**  

  ![image-20200714110338132](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714110338.png)

  ==指定解压到的那个目录， 事先要存在才能成功， 否则会报错。== 

# 第四章   组管理和权限管理

## 4.1 Linux 组基本介绍

​	在 linux 中的每个用户必须属于一个组， 不能独立于组外。 在 linux 中每个文件有所有者、 所在组、 其它组的概念。
​	1) 所有者
​	2) 所在组
​	3) 其它组
​	4) 改变用户所在的组  

![image-20200714110744377](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714110745.png)

## 4.2 文件/目录 所有者  

### 4.2.1 查看文件的所有者

1. 指令： ls -ahl

2. **应用实例：**创建一个组polic，在创建一个用户tom，将tom放在polic组，然后使用tom来创建一个文件ok.txt,看看情况如何

   ![image-20200714111935042](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714111936.png)

![image-20200714112325738](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714112326.png)

### 4.2.3 修改文件所有者

* **指令**

  **chown**	用户名	文件名

* **应用实例**

  要求： 使用root 创建一个文件apple.txt，然后将其所有者修改成 tom

  ![image-20200714112821153](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714112822.png)

## 4.3 组的创建

### 4.3.1 基本指令

​	**groupadd** 组名

### 4.3.2 应用实例

​	创建一个组，monster

​	创建一个用户 fox , 并放入到 monster 组中

​	![image-20200714113128197](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714113130.png)

## 4.4 文件/目录 所在组

​	当某个用户创建了一个文件后， 默认这个文件的所在组就是该用户所在的组。  

### 4.4.1 查看文件/目录所在组  

* **基本指令**

  **ls  -alh**

### 4.4.2 修改文件所在的组

* **基本指令**

  chgrp 组名 文件名

* **应用实例**

  使用 root 用户创建文件 orange.txt ,看看当前这个文件属于哪个组， 然后将这个文件所在组， 修改到 police 组。  

  ![image-20200714113853636](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714113854.png)

## 4.5 其它组  

​	除文件的所有者和所在组的用户外， 系统的其它用户都是文件的其它组.  

## 4.6 改变用户所在组  

​	在添加用户时， 可以指定将该用户添加到哪个组中， 同样的用 root 的管理权限可以改变某个用户所在的组。  

### 4.6.1 改变用户所在组

1. ​	usermod - g  组名   用户名
2. ​    usermod   -d 目录名   用户名    改变该用户登陆的初始目录

### 4.6.2  应用实例

​	![image-20200714114739471](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714114740.png)

## 4.7 权限的基本介绍

​	ls -l 中显示的内容如下：

​	**-rwxrw-r--** 1 root root 1213 Feb 2 09:39 abc  

​	==**0-9 位说明**==

1. 第0位确定文件类型(d, -, c, b)
2. 第1-3位确定所有者（该文件的所有者）拥有该文件的权限。 ---User 
3. 第 4-6 位确定所属组（同用户组的） 拥有该文件的权限， ---Group  
4. 第 7-9 位确定其他用户拥有该文件的权限 ---Other  

![image-20200714115222643](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714115223.png)

## 4.8 rwx 权限的详解

### 4.8.1  rwx 作用到文件

1. [ r ]代表可读(read): 可以读取,查看  
2. [ w ]代表可写(write): 可以修改,但是不代表可以删除该文件,删除一个文件的前提条件是对该文件所在的目录有写权限， 才能删除该文件  
3. [ x ]代表可执行(execute):可以被执行  

### 4.8.2 rwx 作用到目录  

1. [ r ]代表可读(read): 可以读取， ls 查看目录内容  
2. [ w ]代表可写(write): 可以修改,目录内创建+删除+重命名目录  
3. [ x ]代表可执行(execute):可以进入该目录

## 4.9 文件及目录权限的实际案例

​	ls -l 中显示的内容如下： ==(记住)==  

​	**-rwxrw-r-- 1 root root 1213 Feb 2 09:39 abc**  

**10 个字符确定不同用户能对文件干什么**

​	第一个字符代表文件类型： 文件 (-),目录(d),链接(l)
​	其余字符每 3 个一组(rwx) 读(r) 写(w) 执行(x)
​	第一组 rwx : 文件拥有者的权限是读、 写和执行
​	第二组 rw- : 与文件拥有者同一组的用户的权限是读、 写但不能执行
​	第三组 r-- : 不与文件拥有者同组的其他用户的权限是读不能写和执行  

**可用数字表示为: r=4,w=2,x=1 因此 rwx=4+2+1=7**  

| 1           | 文件： 硬连接数或 目录： 子目录数              |
| ----------- | ---------------------------------------------- |
| root        | 用户                                           |
| root        | 组                                             |
| 1213        | 文件大小(字节)， 如果是文件夹， 显示 4096 字节 |
| Feb 2 09:39 | 最后修改日期                                   |
| abc         | 文件名                                         |

## 4.10. 修改权限-chmod

### 4.10.1 基本说明

​	通过chmod指令，可以修改文件或者目录的权限

### 4.10.2  第一种方式： + 、-、= 变更权限

​	u ： 所有者  g: 所有组   o:其他人   a:所有人（u、g、o 的总和）

1. chmod  u= rwx , g = rx , o=x    文件目录名
2. chmod o+w    文件目录名
3. chmod   a-x     文件目录名

* **案例演示**

  1. **给 abc 文件 的==所有者读写执行的权限==， 给==所在组读执行权限==， 给其它组读执行权限。**  

  ![image-20200714121719548](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714121720.png)

  2. **给 abc 文件的所有者除去执行的权限， 增加组写的权限**  

     ![image-20200714121919294](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714121920.png)

### 4.10.3 第二种方式： 通过数字变更权限

​	**规则：** 

​		r=4 w=2 x=1 		rwx=4+2+1=7

​		chmod u=rwx,g=rx,o=x		文件目录名

​		相当于 chmod 	751		文件目录名

* **案例演示**

  **要求： 将 /home/abc.txt 文件的权限修改成 rwxr-xr-x, 使用给数字的方式实现：**  

  **rwx = 4+2+1 = 7       r-x = 4+1=5      r-x = 4+1 =5**  

  ![image-20200714122646171](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714122647.png)

## 4.11 修改文件所有者-chown  

### 4.11.1 基本介绍

​	**chown   newowner  file** 改变文件的所有者

​	**chown   newowner:newgroup  file**   改变用户的所有者和所有组

​	**-R**   如果是目录 则使其下所有的子文件或目录递归生效

### 4.11.2 案例演示

​	1. **请将 /home/abc .txt 文件的所有者修改成 tom**

​	 ![image-20200714123428050](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714123430.png) 	

	2. 请将 /home/kkk 目录下所有的文件和目录的所有者都修改成 tom  ![image-20200714123616286](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714123617.png)

## 4.12  修改文件所在组-chgrp  

### 4.12.1 基本介绍

​	**chgrp newgroup file**   改变文件的所有组 

### 4.12.2 案例演示

​	1.**请将 /home/abc .txt 文件的所在组修改成 bandit (土匪)**  

​	![image-20200714124255800](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714124258.png)

​	2**.请将 /home/kkk 目录下所有的文件和目录的所在组都修改成 bandit(土匪)**  

​	![image-20200714124447588](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714124449.png)

## 4.13 实战练习

**题目：**  **最佳实践-警察和土匪游戏**  

​	police ， bandit

​	jack, jerry: 警察
​	xh, xq: 土匪

**(1) 创建组**

![image-20200714124919507](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714124920.png)

**(2) 创建用户**  

![image-20200714125102237](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714125102.png)

同时给4个用户设置密码：（示例）

​	![image-20200714125148533](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714125149.png)

**(3) jack 创建一个文件， 自己可以读写， 本组人可以读， 其它组没人任何权限**  

![image-20200714130751547](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714130753.png)

**(4) jack 修改该文件， 让其它组人可以读, 本组人可以读写**  

![image-20200714131045468](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714131046.png)

**(5) xh 投靠 警察， 看看是否可以读写.**  

先用 root 修改 xh 的组 ：  

![image-20200714131212914](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714131215.png)

使用 jack 给他的家目录 /home/jack 的所在组一个 rx 的权限  

![image-20200714131538667](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714131539.png)

xh 需要重新注销在到 jack 目录就可以操作 jack 的文件  ![image-20200714132019715](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714132020.png)

# 第五章 crond 任务调度

## 5.1 原理示意图

![image-20200714233237708](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714233238.png)

![image-20200714233255262](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714233256.png)

**crontab 进行 定时任务的设置**

## 5.2 基本语法

​	**crontab** [选项]

### 5.2.1 常用选项

![image-20200714233559033](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714233559.png)

## 5.3 快速入门

### 5.3.1 任务的要求

​	设置任务的调度文件： /ect/crontab

​	设置个人任务调度。执行crontab -e 命令

​	接着输入任务到调度文件

​	如： */1 * * * * ls – l /etc/ > /tmp/to.txt
​	意思说每小时的每分钟执行 ls – l /etc/ > /tmp/to.txt 命令

### 5.3.2 步骤如下

1. cron -e
2. */ 1 * * * * ls -l /etc >> /tmp/to.txt  
3. 保存退出就会启动程序。
4. 在每一分钟都会自动保存的调用 ls -l /etc >> /tmp/to.txt

### 5.3.3 参数细节说明

* 5**个占位符的说明**

![image-20200714235831711](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714235832.png)

* **特殊符号说明**

  ![image-20200714235924290](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200714235929.png)

* **特定时间执行任务案例**

  ![image-20200715000050290](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/20200715000051.png)

## 5.4 任务调度的几个使用案例

### 5.4.1 案例1：

**每隔1分钟，就将当前的日期信息，追加到/tmp/mydate 文件中**

1. 先编写一个文件 /home/mytask1.sh
   	date >> /tmp/mydate
2.  给 mytask1.sh 一个可以执行权限
      	chmod 744 /home/mytask1.sh
3.  crontab -e
4. */1 * * * * /home/mytask1.sh
5.  成功  

### 5.4.2 案例2：

**每隔 1 分钟， 将当前日期和日历都追加到 /home/mycal 文件中**  

1.先编写一个文件 /home/mytask2.sh
	date >> /tmp/mycal
	cal >> /tmp/mycal

2. 给 mytask1.sh 一个可以执行权限
   chmod 744 /home/mytask2.sh
3. crontab -e
4. */1 * * * * /home/mytask2.sh
5. 成功  

### 5.4.3  案例 3:   

**每天凌晨 2:00 将 mysql 数据库 testdb ， 备份到文件中mydb.bak。**  

1. 先编写一个文件 /home/mytask3.sh
   /usr/local/mysql/bin/mysqldump -u root -proot testdb > /tmp/mydb.bak
2. 给 mytask3.sh 一个可以执行权限
   chmod 744 /home/mytask3.sh
3. crontab -e
4. 0 2 * * * /home/mytask3.sh
5. 成功 

## 5.5 crond 相关指令

1. **crontab -r**  :  终止任务调度。
2.  **crontab -l**  :  列出当前有哪些任务调度
3. **service crond restart** :  [重启任务调度]



# 第六章 Linux磁盘分区、挂载

## 6.1 分区基础知识  

### 6.1.1 分区的方式  

**mbr 分区**  

1. 最多支持四个主分区 
2. 系统只能安装在主分区  
3. 扩展分区要占一个主分区
4. MBR 最大只支持 2TB， 但拥有最好的兼容性   

**gtp 分区**   	

1. 支持无限多个主分区（但操作系统可能限制， 比如 windows 下最多 128 个分区）  
2. 最大支持 18EB 的大容量（1EB=1024 PB， 1PB=1024 TB ）
3. windows7 64 位以后支持 gtp  

## 6.2  Linux 分区  

### 6.2.1 原理介绍 

1. Linux 来说无论有几个分区， 分给哪一目录使用， 它归根结底就只有一个根目录， 一个独立且唯一的文件结构 , Linux 中每个分区都是用来组成整个文件系统的一部分。

2. Linux 采用了一种叫“载入” 的处理方法， 它的整个文件系统中包含了一整套的文件和目录，且将一个分区和一个目录联系起来。 这时要载入的一个分区将使它的存储空间在一个目录下获得。

3. **示意图：**    

   ![image-20200716110138982](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716110138982.png)

### 6.2.2 硬盘说明 

1.  Linux 硬盘分 IDE 硬盘和 SCSI 硬盘， 目前基本上是 SCSI 硬盘  
2. 对于 IDE 硬盘， 驱动器标识符为“hdx~”,其中“hd”表明分区所在设备的类型， 这里是指 IDE 硬盘了。 “x”为盘号（a 为基本盘， b 为基本从属盘， c 为辅助主盘， d 为辅助从属盘） ,“~”代表分区，前四个分区用数字 1 到 4 表示， 它们是主分区或扩展分区， 从 5 开始就是逻辑分区。 例， hda3 表示为第一个 IDE 硬盘上的第三个主分区或扩展分区,hdb2 表示为第二个 IDE 硬盘上的第二个主分区或扩展分区。
3. 对于 SCSI 硬盘则标识为“sdx~”， SCSI 硬盘是用“sd”来表示分区所在设备的类型的， 其余则和 IDE 硬盘的表示方法一样。  

### 6.2.3 使用 lsblk 指令查看当前系统的分区情况  

![image-20200716111042744](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716111042744.png)

![image-20200716111125821](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716111125821.png)

## 6.3 挂载的经典案例

**需求是给我们的 Linux 系统增加一个新的硬盘， 并且挂载到/home/newdisk**  

![image-20200716111804631](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716111804631.png)

### 6.3.1 如何增加一块硬盘  

1. 虚拟机添加硬盘  

2. 分区 fdisk /dev/sdb

3. 格式化 mkfs -t ext4 /dev/sdb1

4. 挂载 先创建一个 /home/newdisk , 挂载 mount /dev/sdb1 /home/newdisk

5. 设置可以自动挂载(永久挂载， 当你重启系统， 仍然可以挂载到 /home/newdisk) 。

   vim 		/etc/fstab
   /dev/sdb1 		/home/newdisk		 ext4 			defaults 		0 0

## 6.4  具体的操作步骤整理  

### 6.4.1 虚拟机增加硬盘步骤 1  

​	在【虚拟机】 菜单中， 选择【设置】 ， 然后设备列表里添加硬盘， 然后一路【下一步】 ， 中间只选择磁盘大小的地方需要修改， 至到完成。 然后重启系统（才能识别） ！

![image-20200716114951454](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716114951454.png)

### 6.4.2 虚拟机增加硬盘步骤 2  

​	分区命令 fdisk /dev/sdb
​	开始对/sdb 分区
​	•m  显示命令列表
​	•p  显示磁盘分区 同 fdisk – l
​	•n  新增分区
​		•d  删除分区
​	•w  写入并退出

**==说明：==**开始分区后输入 n， 新增分区， 然后选择 p ， 分区类型为主分区。 两次回车默认剩余全部空间。 最后输入 w 写入分区并退出， 若不保存退出输入 q。

![image-20200716115128699](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716115128699.png)

### 6.4.3 虚拟机增加硬盘步骤 3  

​	格式化磁盘

​	分区命令:mkfs -t ext4 	 /dev/sdb1
​	其中 ext4 是分区类型

### 6.4.4 虚拟机增加硬盘步骤 4  

​	挂载: 将一个分区与一个目录联系起来，
​	•mount 	设备名称 	挂载目录
​	•例如： mount 	/dev/sdb1	 /newdisk
​	•==umount 设备名称 	或者 	挂载目录==

### 6.4.5 虚拟机增加硬盘步骤 5  

​	永久挂载: 通过修改/etc/fstab 实现挂载
​	添加完成后 执行 mount  	– a	 即刻生效   

![image-20200716115319818](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716115319818.png)

## 6.5 磁盘情况查询  

### 6.5.1 查询系统整体磁盘使用情况  

* **基本语法**

  **df  -h**  

* **应用实例**  

  查询系统整体磁盘使用情况  

  ![image-20200716115832997](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716115832997.png)

### 6.5.2  查询指定目录的磁盘占用情况  

* **基本语法**  

  **du -h** / 目录  

  查询指定目录的磁盘占用情况， 默认为当前目录 

  | 指令          | 描述                        |
  | ------------- | --------------------------- |
  | -s            | 指定目录占用大小汇总        |
  | -h            | 带计量单位                  |
  | -a            | 含文件                      |
  | --max-depth=1 | 子目录深度                  |
  | -c            | 列出明细的同时， 增加汇总值 |

### 6.6 磁盘情况-工作实用指令  

1. **统计/home 文件夹下文件的个数**  

   ![image-20200716120414567](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716120414567.png)

2. **统计/home 文件夹下目录的个数**  

   ![image-20200716120602354](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716120602354.png)

3. **统计/home 文件夹下文件的个数， 包括子文件夹里的**  

   ![image-20200716120722475](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716120722475.png)

4. **统计文件夹下目录的个数， 包括子文件夹里的**  

   ![image-20200716120936908](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716120936908.png)

5. **以树状显示目录结构**  （CenOS 7）

   ![image-20200716121248128](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716121248128.png)

![image-20200716121347618](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716121347618.png)

# 第七章 网络配置  

## 7.1 Linux 网络配置原理图(含虚拟机) 

**目前我们的网络配置采用的是 NAT。**  

![image-20200716125541980](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716125541980.png)

## 7.2 查看网络 IP 和网关  

### 7.2.1 查看虚拟网络编辑器  

![image-20200716125906761](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716125906761.png)

### 7.2.2 修改 ip 地址(修改虚拟网络的 ip)  

![image-20200716130339488](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716130339488.png)

### 7.2.3 查看网关

![image-20200716130444151](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716130444151.png)

### 7.2.4 查看 windows 环境的中 VMnet8 网络配置 (ipconfig 指令)  

1.  使用 ipconfig 查看  

2. 界面查看

   ![image-20200716131037431](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716131037431.png)  

## 7.3 ping 测试主机之间网络连通  

### 7.3.1 基本语法  

​	**ping** 目的主机 （功能描述： 测试当前服务器是否可以连接目的主机）  

### 7.3.2 应用实例  

​	**测试当前服务器是否可以连接百度**  

​	![image-20200716131643211](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716131643211.png)

## 7.4 linux 网络环境配置  

### 7.4.1 指定固定的 ip  

**说明**  

​	直 接 修 改 配 置 文 件 来 指 定 IP, 并 可 以 连 接 到 外 网 ( 程 序 员 推 荐 ) ， 编 辑 

```bash
vi  /etc/sysconfig/network-scripts/ifcfg-eth0
```

**要求： 将 ip 地址配置的静态的， ip 地址为 192.168.184.130**   (IP地址参看自己的)

```bash
ifconfig //在Linux终端即可查看
```

![image-20200716162207894](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716162207894.png)

**修改后， 一定要 ==重启服务==**  

```bash
service network restart
```

```
reboot 重启系统
```

![image-20200716162338058](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716162338058.png)

# 第八章  进程管理  

## 8.1 显示系统执行的进程  

### 8.1.1 说明

​	查看进行使用的指令是 ps ,一般来说使用的参数是 **ps -aux**  

​	![image-20200716162932629](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716162932629.png)

![image-20200716162953140](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716162953140.png)

### 8.1.2 ps 指令详解

1. 指令： ps – aux|grep xxx ， 比如我看看有没有 sshd 服务  

2. 指令说明

   | 指令     | 描述                                                         |
   | -------- | ------------------------------------------------------------ |
   | System V | 展示风格                                                     |
   | USER     | 用户名称                                                     |
   | PID      | 进程号                                                       |
   | %CPU     | 进程占用 CPU 的百分比                                        |
   | %MEM     | 进程占用物理内存的百分比                                     |
   | VSZ      | 进程占用的虚拟内存大小（单位： KB）                          |
   | RSS      | 进程占用的物理内存大小（单位： KB）                          |
   | TT       | 终端名称,缩写                                                |
   | STAT     | 进程状态， 其中 S-睡眠， s-表示该进程是会话的先导进程， N-表示进程拥有比普通优先级更低的优先级， R-正在运行， D-短期等待， Z-僵死进程， T-被跟踪或者被停止等等 |
   | STARTED  | 进程的启动时间                                               |
   | TIME     | CPU 时间， 即进程使用 CPU 的总时间                           |
   | COMMAND  | 启动进程所用的命令和参数， 如果过长会被截断显示              |

### 8.1.3 应用实例  

*  **要求： 以全格式显示当前所有的进程， 查看进程的父进程。**  

![image-20200716163908090](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716163908090.png)

```bash
ps -ef 是以全格式显示当前所有的进程
-e 显示所有进程。 -f 全格式
```

* **ps -ef| grep xxx   是 BSD 风格**  

| 方法  | 描述                                                         |
| ----- | ------------------------------------------------------------ |
| UID   | 用户 ID                                                      |
| PID   | 进程 ID                                                      |
| PPID  | 父进程 ID                                                    |
| C     | CPU 用于计算执行优先级的因子。 数值越大， 表明进程是 CPU 密集型运算， 执行优先级会<br/>降低； 数值越小， 表明进程是 I/O 密集型运算， 执行优先级会提高 |
| STIME | 进程启动的时间                                               |
| TTY   | 完整的终端名称                                               |
| TIME  | CPU 时间                                                     |
| CMD   | 启动进程所用的命令和参数                                     |

* **要求：查看 sshd 进程的父进程号是多少， 应该怎样查询**   

![image-20200716164558921](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716164558921.png)

## 8.2 终止进程 kill 和 killall  

### 8.2.1 介绍:  

​	若是某个进程执行一半需要停止时， 或是已消了很大的系统资源时， 此时可以考虑停止该进程。使用 kill 命令来完成此项任务。  

### 8.2.1 基本语法  

​	**kill** [选项] 进程号（功能描述： 通过进程号杀死进程）  

​	**killall** 进程名称 （功能描述： 通过进程名称杀死进程， 也支持通配符， 这在系统因负载过大而变得很慢时很有用）  

### 8.2.2 常用选项  

​	**-9** :表示强迫进程立即停止  

### 8.2.3 最佳实践  

​	**案例 1： 踢掉某个非法登录用户**  

![image-20200716165539424](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716165539424.png)

​	**案例 2: 终止远程登录服务 sshd, 在适当时候再次重启 sshd 服务**  

​	![image-20200716165722306](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716165722306.png)

​	**案例 3: 终止多个 gedit 编辑器 【killall , 通过进程名称来终止进程】**  

​	![image-20200716165929281](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716165929281.png)

 	**案例 4： 强制杀掉一个终端**  		![image-20200716170008099](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716170008099.png)

## 8.3 查看进程树 pstree  

### 8.3.1 基本语法  

​	**pstree** [选项] ,可以更加直观的来看进程信息  

### 8.3.2 常用选项  

​	**-p** :显示进程的 PID

​	**-u** :显示进程的所属用户 

### 8.3.3 应用实例  

​	**案例 1： 请你树状的形式显示进程的 pid**  

​	![image-20200716170418195](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716170418195.png)

​	**案例 2： 请你树状的形式进程的用户 id**  

​	![image-20200716170522289](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716170522289.png)

## 8.4 服务(Service)管理

### 8.4.1 介绍

​	服务(service) 本质就是进程， 但是是运行在后台的， 通常都会监听某个端口， 等待其它程序的请求， 比如(mysql , sshd 防火墙等)， 因此我们又称为守护进程， 是 Linux 中非常重要的知识点。 【原理图】  

![image-20200716170655510](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716170655510.png)

### 8.4.2 service 管理指令  

​	**service** 服务名 [start | stop | restart | reload | status]

​	在 CentOS7.0 后 不再使用 service ,而是 **systemctl**	

### 8.4.3 使用案例  

**==CentOS 7== 示例：**

```bash
# 查看firewall服务状态   
systemctl status firewalld
# 开启
service firewalld start
# 重启
service firewalld restart
# 关闭
service firewalld stop

# 查看防火墙规则
firewall-cmd --list-all 

# 查询端口是否开放
firewall-cmd --query-port=8080/tcp
# 开放80端口
firewall-cmd --permanent --add-port=80/tcp
# 移除端口
firewall-cmd --permanent --remove-port=8080/tcp

#重启防火墙(修改配置后要重启防火墙)
firewall-cmd --reload

# 参数解释
1、firwall-cmd：是Linux提供的操作firewall的一个工具；
2、--permanent：表示设置为持久；
3、--add-port：标识添加的端口；
```

1. **查看当前防火墙的状况， 关闭防火墙和重启防火墙。**  

   ![image-20200716171940787](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716171940787.png)

![image-20200716173533184](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716173533184.png)

![image-20200716173556479](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716173556479.png)

**==CenOS 6:==**

![image-20200716173638162](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716173638162.png)

### 8.4.4 细节讨论  

1. **关闭或者启用防火墙后， 立即生效。 [telnet 测试 某个端口即可]**  

   ![image-20200716173742478](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716173742478.png)

2. **这种方式只是临时生效， 当重启系统后， 还是回归以前对服务的设置。**  

### 8.4.5 查看服务名  

​	**方式 1： 使用 setup -> 系统服务 就可以看到。**  

​	![image-20200716174037167](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716174037167.png)

**方式 2: /etc/init.d/服务名称**  

​	![image-20200716174233887](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716174233887.png)

### 8.4.6  服务的运行级别(runlevel)  

​	查看或者修改默认级别： vi /etc/inittab
​	Linux 系统有 7 种运行级别(runlevel)： 常用的是级别 3 和 5  

* 运行级别 0： 系统停机状态， 系统默认运行级别不能设为 0， 否则不能正常启动
* 运行级别 1： 单用户工作状态， root 权限， 用于系统维护， 禁止远程登陆
* 运行级别 2： 多用户状态(没有 NFS)， 不支持网络
* 运行级别 3： 完全的多用户状态(有 NFS)， 登陆后进入控制台命令行模式
* 运行级别 4： 系统未使用， 保留
* 运行级别 5： X11 控制台， 登陆后进入图形 GUI 模式
* 运行级别 6： 系统正常关闭并重启， 默认运行级别不能设为 6， 否则不能正常启动  

### 8.4.7 开机的流程说明  

![image-20200716174511184](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716174511184.png)

### 8.4.8 chkconfig 指令  

* **介绍**  

  通过 chkconfig 命令可以给每个服务的各个运行级别设置自启动/关闭  

* **基本语法**  (==CenOS 6==)

  1. **查看服务 chkconfig --list|grep xxx**  

     ![image-20200716174754465](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716174754465.png)

![image-20200716174925168](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716174925168.png)

2. **chkconfig 服务名 --list**  

   ![image-20200716175226244](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716175226244.png)

3. **chkconfig --level 5 服务名 on/off**  

   请将 sshd 服务在运行级别为 5 的情况下， 不要自启动。  

   ![image-20200716175304029](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716175304029.png)

### 8.4.9 应用实例  (CenOS 6)

​	**案例 1： 请显示当前系统所有服务的各个运行级别的运行状态**  

~~~bash
chkconfig --list
~~~

​	**案例 2 ： 请查看 sshd 服务的运行状态**  

```
 service sshd status
```

​	**案例 3： 将 sshd 服务在运行级别 5 下设置为不自动启动， 看看有什么效果？**  

```bash
chkconfig --level 5 sshd off
```

​	**案例 4： 当运行级别为 5 时， 关闭防火墙。**

```bash
 chkconfig --level 5 iptables off
```

  **案例 5： 在所有运行级别下， 关闭防火墙**

```bash
chkconfig iptables off
```

​	**案例 6： 在所有运行级别下， 开启防火墙**  

```bash
 chkconfig iptables on
```

### 8.4.10 使用细节  

chkconfig 重新设置服务后自启动或关闭， 需要重启机器 **reboot** 才能生效.  

## 8.5 动态监控进程  

### 8.5.1 介绍  

​	top 与 ps 命令很相似。 它们都用来显示正在执行的进程。 Top 与 ps 最大的不同之处， 在于 top 在执行一段时间可以更新正在运行的的进程。  

### 8.5.2 基本语法  

​	**top** [选项]  

### 8.5.3 选项说明  

![image-20200716180318802](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716180318802.png)

![image-20200716180340901](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716180340901.png)

### 8.5.4 应用实例  

​	**案例 1.监视特定用户**  

top： 输入此命令， 按回车键， 查看执行的进程。

u： 然后输入==“u” 回车， 再输入用户名， 即可==  

![image-20200716180954926](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716180954926.png)

​	**案例 2： 终止指定的进程**  

​	top： 输入此命令， 按回车键， 查看执行的进程。
​	k： 然后输入“k” 回车， 再输入要结束的进程 ID 号  

![image-20200716181038036](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716181038036.png)

**案例 3:指定系统状态更新的时间(每隔 10 秒自动更新， 默认是 3 秒)**  

```bash
 top -d 10
```

### 8.5.5 查看系统网络情况 netstat(重要)  

* **基本语法**  

  **netstat** [选项]
  **netstat -anp**

* **选项说明**  

  **-an**  	按一定顺序排列输出
  **-p** 		显示哪个进程在调用  

* **应用案例**  (==CenOS 6==)

  **查看系统所有的网络服务**  

  ![image-20200716181511135](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716181511135.png)

  **请查看服务名为 sshd 的服务的信息。**

  ![image-20200716181546012](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716181546012.png)  

# 第九章 RPM 和 YUM  

## 9.1 rpm 包的管理  

### 9.1.1 rpm 包的简单查询指令  

​	查询已安装的 rpm 列表 rpm – qa|grep xx

​	请查询看一下， 当前的 Linux 有没有安装 firefox .  

![image-20200716182049241](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716182049241.png)

### 9.1.2 rpm 包名基本格式  

​	一个 rpm 包名： firefox-45.0.1-1.el6.centos.x86_64.rpm
​	名称:firefox
​	版本号： 45.0.1-1
​	适用操作系统: el6.centos.x86_64
​	表示 centos6.x 的 64 位系统
​	如果是 i686、 i386 表示 32 位系统， noarch 表示通用。 。  

### 9.1.3 rpm 包的其它查询指令  

​	**rpm -qa** :查询所安装的所有 rpm 软件包  

​	**rpm -qa | more** [分页显示]  

​	**rpm -qa | grep X [rpm -qa** | grep firefox ]  

​	![image-20200716182436952](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716182436952.png)

​	**rpm -q** 软件包名 :查询软件包是否安装  

​	![image-20200716182607417](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716182607417.png)

​	**rpm -qi** 软件包名 ： 查询软件包信息  

​	![image-20200716183009944](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716183009944.png)

​	**rpm -ql** 软件包名 :查询软件包中的文件  

​	![image-20200716183224931](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716183224931.png)

​	**rpm -qf** 文件全路径名 查询文件所属的软件包 

​	rpm -qf /etc/passwd
​	rpm -qf /root/install.log   

![image-20200716183527562](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716183527562.png)

### 9.1.4 卸载 rpm 包  

* **基本语法**  

  ​	**rpm -e RPM** 包的名称  

* **应用案例**  
  
  1.  删除 firefox 软件包  

![image-20200716183708154](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716183708154.png)

* **细节问题**  

  1.  如果其它软件包依赖于您要卸载的软件包， 卸载时则会产生错误信息。  

     如： $ rpm -e foo  

     removing these packages would break dependencies:foo is needed by bar-1.0-1  

  2. 如果我们就是要删除 foo 这个 rpm 包， 可以增加参数 --nodeps ,就可以强制删除， 但是一般不推荐这样做， 因为依赖于该软件包的程序可能无法运行  

     如： $ rpm -e ==--nodeps== foo
     带上 ==--nodeps== 就是强制删除。  

### 9.1.5 安装 rpm 包  

* **基本语法**  

  **rpm -ivh RPM** 包全路径名称  

* **参数说明**  

  **i=install** 		安装
  **v=verbose**		 提示
  **h=hash** 			进度条  

* **应用实例**  

  1. 演示安装 firefox 浏览器  

     步骤先找到 firefox 的安装 rpm 包,你需要挂载上我们安装 centos 的 iso 文件， 然后到/media/下去找 rpm 找。

     cp firefox-45.0.1-1.el6.centos.x86_64.rpm   /opt/    

     ![image-20200716184254683](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716184254683.png)

## 9.2 yum

### 9.2.1 介绍

​	Yum 是一个 Shell 前端软件包管理器。 基于 RPM 包管理， 能够从指定的服务器自动下载 RPM 包并且安装， 可以自动处理依赖性关系， 并且一次安装所有依赖的软件包。 使用 yum 的前提是可以联网。

  	

![image-20200716225141213](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716225141213.png)

### 9.2.2 yum 的基本指令  

* **查询 yum 服务器是否有需要安装的软件**  

  **yum list|grep xx** 软件列表   软件列表  

* **安装指定的 yum 包**  

  **yum install xxx** 下载安装  

### 9.2.3 yum 应用实例  

​	**案例： 请使用 yum 的方式来安装 firefox**  

​	**1.先查看一下 firefox rpm 在 yum 服务器有没有**  

~~~bash
rpm -e firefox
~~~

​	![image-20200716225743794](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716225743794.png)

2. **安装**  

```bash
yum install firefox
```

​	会安装最新版本的软件  

​	【完成】

![image-20200716230040138](https://gitee.com/oy_chart_bed/no1_drawing_bed/raw/master/image-20200716230040138.png)

