简易购物车项目简介
=


如需源码请联系[程序帮](http://ll032.cn/HZ6vHa)：QQ1022287044


开发环境：
----
1. jdk1.8
2. tomcat8
3. mysql
4. intellij IDEA

1.项目开发准备:
-----
1. 创建github仓库
2. 项目框架搭建
3. 项目构建并同步仓库
4. 编写所需业务逻辑

2.开发项目解决方案:
-----
1. github仓库站上所属存放的项目仓库
2. mysql数据库中创建项目所需shopCartDB数据库，用于储存购物车项目所需数据
4. 采用注解@WebServlet进行http请求响应
3. 搭建jsp+servlet架构的技术框架，基于c标签及el表达式进行jsp页面数据渲染,
c标签引入方式：
```diff
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```
 根据jdbc直连技术，编写数据库操作工具类，方便存储数据，代码如下：
```
public class DBUtils {
	String url = null;		//连接地址
	String username = null;		//数据库名
	String password = null;		//数据库密码
	String driverClass = null;	//连接驱动
	private static DBUtils db = new DBUtils();
	/**构建数据库连接参数*/
	private DBUtils() {
		try {
			url = "jdbc:mysql://localhost:3306/shopCartDb?useUnicode=true&characterEncoding=utf8";
			username = "root";
			password = "root123";
			driverClass = "com.mysql.jdbc.Driver";
			Class.forName(driverClass);
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
	/**构建数据库连接对象*/
	public Connection getConnection(){
		Connection conn = null;
		try {
			conn = DriverManager.getConnection(url, username, password);
		} catch (Exception e) {
			e.printStackTrace();
		}
		return conn;
	}
	public static DBUtils getInstance(){
		return db;
	}
}
```


3.项目功能:
-----
1. 注册
2. 登录
3. 找回密码
4. 商品列表
5. 添加购物车
6. 购物车删除
7. 购物车数量修改
8. 购物车结算

4.开发内容：
---

本项目采用mysql数据库进行储存数据，所以优先搭建项目所需数据库结构，此项目有用户表，商品表，购物车表，结算表等信息。<br>
利用搭建好的jsp+servlet框架提供http请求及响应视图能力，展示项目所需各个jsp页面。根据响应显示注册页面进行注册操作。<br>
根据注册所填写的帐号和密码进行系统登录，如忘记密码，可根据邮件动态验证码形式进行密码找回，密码采用腾讯QQ服务提供的SMTP服务器<br>
进行验证码收发操作，系统进入后展示商品列表，利用c标签将db入库的数据进行动态渲染，el表达式进行数据取值展示，添加购物车利用ajax请求<br>
进行添加购物车、移除购物车的技术实现，根据所添加的购物车列表数据，可更改购物车的数量进行结算，将购物车页面数据进行复选框勾选模式。<br>
可进行多个商品一起结算，利用js技术筛选出具体哪些商品进行勾选，根据勾选商品的数量及商品单价进行最终价格结算。从而完成一系列的购物车<br>
技术实现<br>

5.部分代码截图:
-----

- 商品列表代码

![商品列表代码](https://github.com/chengxubang/JSP/blob/main/image/%E4%BB%A3%E7%A0%81%E6%88%AA%E5%9B%BE/%E5%95%86%E5%93%81%E5%88%97%E8%A1%A8%E4%BB%A3%E7%A0%81.png)

- 购物车列表代码

![购物车列表代码](https://github.com/chengxubang/JSP/blob/main/image/%E4%BB%A3%E7%A0%81%E6%88%AA%E5%9B%BE/%E8%B4%AD%E7%89%A9%E8%BD%A6%E5%88%97%E8%A1%A8%E4%BB%A3%E7%A0%81.png)

- 结算后端代码

![结算后端代码](https://github.com/chengxubang/JSP/blob/main/image/%E4%BB%A3%E7%A0%81%E6%88%AA%E5%9B%BE/%E7%BB%93%E7%AE%97%E5%90%8E%E7%AB%AF%E4%BB%A3%E7%A0%81.png)

- 结算列表代码

![结算列表代码](https://github.com/chengxubang/JSP/blob/main/image/%E4%BB%A3%E7%A0%81%E6%88%AA%E5%9B%BE/%E7%BB%93%E7%AE%97%E5%88%97%E8%A1%A8%E4%BB%A3%E7%A0%81.png)

6.项目效果:
-----
- 注册

![注册](https://github.com/chengxubang/JSP/blob/main/image/%E7%95%8C%E9%9D%A2%E6%88%AA%E5%9B%BE/%E6%B3%A8%E5%86%8C.png)

- 商品列表

![商品列表](https://github.com/chengxubang/JSP/blob/main/image/%E7%95%8C%E9%9D%A2%E6%88%AA%E5%9B%BE/%E5%95%86%E5%93%81%E5%88%97%E8%A1%A8.png)

- 购物车列表

![购物车列表](https://github.com/chengxubang/JSP/blob/main/image/%E7%95%8C%E9%9D%A2%E6%88%AA%E5%9B%BE/%E8%B4%AD%E7%89%A9%E8%BD%A6%E5%88%97%E8%A1%A8.png)

- 购物车删除

![购物车删除](https://github.com/chengxubang/JSP/blob/main/image/%E7%95%8C%E9%9D%A2%E6%88%AA%E5%9B%BE/%E5%88%A0%E9%99%A4%E8%B4%AD%E7%89%A9%E8%BD%A6.png)

- 购物车结算

![购物车结算](https://github.com/chengxubang/JSP/blob/main/image/%E7%95%8C%E9%9D%A2%E6%88%AA%E5%9B%BE/%E5%88%A0%E9%99%A4%E8%B4%AD%E7%89%A9%E8%BD%A6.png)


7.项目总结:
-----
1. jsp+servlet组合框架开发，条理清晰的mvc框架
2. 了解c标签进行数据渲染及多方面的强大渲染能力，可以更合理动态展示复杂的数据结构
3. 丰富学习了markdown扩充的语法,可以更直观展示项目介绍文档
4. 合理利用jdbc直连技术，更加熟悉掌握对数据的增删改查操作
5. 巩固java的基础知识，并针对不足之处记性额外补充学习，比如list结构及数组结构体的运用
6. 熟悉ajax技术，能利用ajax技术针对get与post请求进行数据的传递和响应

