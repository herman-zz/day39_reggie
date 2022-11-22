瑞吉外卖项目环境搭建：
	1.数据库环境准备
		方式一：DOS命令行实现：
			1.1：登录MySQL数据库服务器  mysql-uroot -proot
			1.2：创建数据库        create  database reggie;
			1.3：切换数据库        use reggie;
			1.4：执行SQL脚本       source D:\db_reggie.sql
		方式二：图形化工具 idea：
			1.1：创建数据库 	reggie
			1.2：执行SQL脚本

	2.项目环境搭建
		1.创建一个普通的maven工程  项目名称为day39_reggie
		2.使用资料中提供的pom.xml替换项目中的pom.xml
		3.拷贝资料中提供的application.yml到项目的resources目录下
		4.编写启动类
			@Slf4j
			@SpringBootApplication
			public class ReggieApplication {
				public static void main(String[] args) {
					SpringApplication.run(ReggieApplication.class,args);
					log.info("项目启动成功！");
				}
			}
		5.OK 可以测试了

		添加静态资源到项目中
			方式一：【后续使用会有问题】
				1.1：直接在resources目录下创建static目录  将静态资源放入static目录中即可
					 原理：
						就是SpringBoot自动配置，因为SpringBoot自动做了静态资源处理
						如果发现你请求的是静态资源 会自动的去到static目录下找对应的资源
					 不推荐原因：如果后面还需要对SpringMVC做配置修改，则会导致SpringBoot中关于SpringMVC的一些自动配置失效  就会导致访问404


			方式二：【推荐】
				2.1：直接将静态资源放到resources目录下 【此时当你访问静态资源时SpringBoot并不知道去哪里找】
				2.2：配置静态资源映射处理  告诉静态资源请求 去哪里找到对应的资源
				@Slf4j
				@Configuration
				public class WebMvcConfig extends WebMvcConfigurationSupport {
					//配置静态资源映射
					@Override
					protected void addResourceHandlers(ResourceHandlerRegistry registry) {
						log.info("开启静态资源映射...");
						registry.addResourceHandler("/backend/**").addResourceLocations("classpath:/backend/");
						registry.addResourceHandler("/front/**").addResourceLocations("classpath:/front/");
					}
				}
瑞吉外卖项目功能开发：
day01：
    后台员工登录
        需求分析：
            1.前端页面：src/main/resources/backend/page/login/login.html
            2.请求流程：输入用户名和密码---->点击登录按钮---->发起请求
            3.接口设计
                请求地址：/employee/login        eg:http://localhost:8080/employee/login
                请求方式：post
                请求参数：{username: "admin", password: "123456"}  json对象格式
                响应数据：登录成功的员工对象 Employee对象
            4.数据模型：employee表
        代码准备：
            前端：
                login.html：点击登录按钮 在handleLogin函数中发送ajax请求
                backend/api/login.js 封装定义了登录请求的API方法
            后端：
                controller：EmployeeController
                service：EmployeeService 、EmployeeServiceImpl
                dao： EmployeeDao
                bean：Employee
                common：R

    后台退出登录：


    完善登录功能：


    新增员工功能：