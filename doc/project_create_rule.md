# 1.pom文件

与项目的基本信息相关的标签有很多，以下算**必填项**:

- `groupId`：项目的组名，通常是反转的域名，比如com.example。
- `artifactId`：项目的唯一标识符，通常是项目的名称。
- `version`：项目的版本号。
- `packaging`：项目的打包方式，通常是**jar**、**war**或**pom**，如果没有指定packaging，默认值是jar（我们的工程暂时只需要支持jar，别的不可选）。

除了上面的几个标签，还有一些项目相关，但**非必填**的内容：

- `name`：项目名，可选项，提供项目的简短名称
- `description`：项目描述，可选项，提供项目的详细描述。
- `version`：项目主页，可选项，提供项目的网址。
- `licenses`： 许可证声明，可选项，声明项目所使用的一种或多种许可证
- `developers`：开发者信息，可选项，列出项目的开发人员。
- `url`：项目主页，可选项，提供项目的网址

# 2. 后端目录结构

 project-root/
├── pom.xml
└── src/
└── main/
├── java/
│ └── com/
│ └── example/
│ ├── Application.java # 启动类
│ ├── common/ # 公共包
│ ├── config/ # 配置包
│ └── modules/ # 业务模块包
└── resources/
├── static/ # 静态资源
├── templates/ # 模板文件（可选）
├── application.yml # 主配置文件
├── application-dev.yml # 开发环境配置
├── application-test.yml # 测试环境配置
├── application-prod.yml # 生产环境配置
└── logback-spring.xml # 日志配置（可选） 

一个具体的示例：

 com/example/
├── Application.java # Spring Boot启动类
├── common/ # 公共模块
│ ├── annotation/ # 自定义注解
│ ├── constant/ # 常量定义
│ ├── exception/ # 全局异常类
│ ├── utils/ # 工具类
│ └── enums/ # 枚举类
├── config/ # 配置模块
│ ├── WebConfig.java # Web配置
│ ├── SwaggerConfig.java # Swagger配置
│ ├── SecurityConfig.java # 安全配置
│ ├── DataSourceConfig.java # 数据源配置
│ └── JpaConfig.java # JPA配置
└── modules/ # 业务模块目录
├── user/ # 用户模块（示例）
│ ├── controller/ # 控制器层
│ ├── service/ # 服务接口
│ │ └── impl/ # 服务实现
│ ├── repository/ # JPA仓库接口
│ ├── model/ # 数据模型
│ │ ├── entity/ # JPA实体(DO)
│ │ ├── dto/ # 数据传输对象
│ │ └── vo/ # 视图对象
│ └── mapper/ # 对象转换接口
└── product/ # 产品模块（示例）
└── ... # 结构同上 