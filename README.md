# Rocket Boot 项目文件功能说明文档

## 项目概述

这是一个用来生成前后端代码的脚手架项目，采用前后端分离架构设计。后端使用JDK17 + SpringBoot3.4 + Spring Data JPA + SQLite等技术，前端使用Vue3 + Element Plus + Ant Design。

## 目录结构

```
rocket-boot-project/
├── README.md                          # 项目说明文档
├── database_field_types.md            # 数据库字段类型配置文档
├── test0725.md                        # 测试需求文档
├── test0725_claude.md                 # 需求解决方案文档
├── PROJECT_FILE_STRUCTURE.md          # 本文档 - 项目文件功能说明
├── rocket-boot/                       # 后端Spring Boot项目
└── ui/                               # 前端Vue3项目
```

## 后端项目结构 (rocket-boot/)

### 配置文件

| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `pom.xml` | Maven配置文件 | 管理项目依赖、插件配置、项目信息 |
| `src/main/resources/application.yml` | Spring Boot配置文件 | 数据库连接、JPA配置、Redis配置等 |
| `rocket-boot.db` | SQLite数据库文件 | 存储用户数据、数据库配置、代码生成任务等 |

### Java源码目录结构

#### 主入口
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `src/main/java/com/guhuo/rocketboot/RocketBootApplication.java` | Spring Boot启动类 | 项目主入口，配置自动扫描和启动 |

#### 通用组件 (common/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `common/ApiResponse.java` | 统一API响应格式 | 封装接口返回数据的统一格式，包括状态码、消息、数据 |

#### 配置类 (config/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `config/ApplicationInitializer.java` | 应用初始化配置 | 项目启动时的初始化逻辑，如数据库初始化 |
| `config/FreemarkerConfig.java` | FreeMarker模板引擎配置 | 配置代码生成模板引擎，设置模板路径和编码 |
| `config/Knife4jConfig.java` | Knife4j API文档配置 | 配置Swagger/Knife4j API文档生成 |
| `config/RedisConfig.java` | Redis配置 | 配置Redis连接和序列化方式 |
| `config/SecurityConfig.java` | Spring Security安全配置 | 配置JWT认证、跨域、安全策略 |

#### 控制器 (controller/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `controller/AuthController.java` | 用户认证控制器 | 处理用户注册、登录、JWT令牌管理 |
| `controller/CodeGenerationController.java` | 代码生成控制器 | 处理代码生成任务、表配置、字段配置等业务 |
| `controller/DatabaseConfigController.java` | 数据库配置控制器 | 管理数据库类型和字段类型配置 |

#### 数据传输对象 (dto/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `dto/CodeGenerationTaskRequest.java` | 代码生成任务请求DTO | 封装创建/更新代码生成任务的请求参数 |
| `dto/DatabaseFieldTypeRequest.java` | 数据库字段类型请求DTO | 封装数据库字段类型配置的请求参数 |
| `dto/DatabaseTypeRequest.java` | 数据库类型请求DTO | 封装数据库类型配置的请求参数 |
| `dto/FieldConfigRequest.java` | 字段配置请求DTO | 封装表字段配置的请求参数 |
| `dto/LoginRequest.java` | 登录请求DTO | 封装用户登录请求参数 |
| `dto/LoginResponse.java` | 登录响应DTO | 封装用户登录响应数据（包含JWT令牌） |
| `dto/RegisterRequest.java` | 注册请求DTO | 封装用户注册请求参数 |
| `dto/TableConfigRequest.java` | 表配置请求DTO | 封装数据库表配置的请求参数 |

#### 实体类 (entity/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `entity/CodeGenerationTask.java` | 代码生成任务实体 | 表示代码生成任务，包含任务信息、步骤、状态等 |
| `entity/DatabaseFieldType.java` | 数据库字段类型实体 | 表示数据库字段类型配置，如VARCHAR、INT等 |
| `entity/DatabaseType.java` | 数据库类型实体 | 表示数据库类型，如MySQL、SQLite、达梦 |
| `entity/FieldConfig.java` | 字段配置实体 | 表示表字段配置，包含字段名、类型、约束等 |
| `entity/ServiceMethodConfig.java` | Service方法配置实体 | 表示Service方法配置，用于生成Service接口 |
| `entity/TableConfig.java` | 表配置实体 | 表示数据库表配置，包含表名、类名、描述等 |
| `entity/User.java` | 用户实体 | 表示系统用户，包含用户名、密码、角色等 |

#### 数据访问层 (repository/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `repository/CodeGenerationTaskRepository.java` | 代码生成任务数据访问 | 提供代码生成任务的数据库操作接口 |
| `repository/DatabaseFieldTypeRepository.java` | 数据库字段类型数据访问 | 提供数据库字段类型的数据库操作接口 |
| `repository/DatabaseTypeRepository.java` | 数据库类型数据访问 | 提供数据库类型的数据库操作接口 |
| `repository/FieldConfigRepository.java` | 字段配置数据访问 | 提供字段配置的数据库操作接口 |
| `repository/ServiceMethodConfigRepository.java` | Service方法配置数据访问 | 提供Service方法配置的数据库操作接口 |
| `repository/TableConfigRepository.java` | 表配置数据访问 | 提供表配置的数据库操作接口 |
| `repository/UserRepository.java` | 用户数据访问 | 提供用户的数据库操作接口 |

#### 安全相关 (security/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `security/JwtAuthenticationEntryPoint.java` | JWT认证入口点 | 处理未认证请求的异常处理 |
| `security/JwtAuthenticationFilter.java` | JWT认证过滤器 | 拦截请求验证JWT令牌 |

#### 业务逻辑层 (service/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `service/CodeGenerationService.java` | 代码生成服务接口 | 定义代码生成相关的业务逻辑接口 |
| `service/CodeTemplateService.java` | 代码模板服务接口 | 定义代码模板生成的业务逻辑接口 |
| `service/DatabaseConfigService.java` | 数据库配置服务接口 | 定义数据库配置管理的业务逻辑接口 |
| `service/JpaQueryBuilderService.java` | JPA查询构建服务接口 | 定义JPA查询方法构建的业务逻辑接口 |
| `service/ServiceMethodGeneratorService.java` | Service方法生成服务接口 | 定义Service方法生成的业务逻辑接口 |
| `service/UserService.java` | 用户服务接口 | 定义用户管理的业务逻辑接口 |

#### 业务逻辑实现 (service/impl/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `service/impl/CodeGenerationServiceImpl.java` | 代码生成服务实现 | 实现代码生成任务管理、表配置、字段配置等业务逻辑 |
| `service/impl/CodeTemplateServiceImpl.java` | 代码模板服务实现 | 实现基于FreeMarker的代码模板生成逻辑 |
| `service/impl/DatabaseConfigServiceImpl.java` | 数据库配置服务实现 | 实现数据库类型和字段类型的配置管理逻辑 |
| `service/impl/JpaQueryBuilderServiceImpl.java` | JPA查询构建服务实现 | 实现JPA查询方法的自动构建逻辑 |
| `service/impl/ServiceMethodGeneratorServiceImpl.java` | Service方法生成服务实现 | 实现Service方法配置的自动生成逻辑 |
| `service/impl/UserServiceImpl.java` | 用户服务实现 | 实现用户注册、登录、认证等逻辑 |

#### 工具类 (util/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `util/JwtUtil.java` | JWT工具类 | 提供JWT令牌的生成、解析、验证功能 |

#### 代码生成模板 (resources/templates/code/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `resources/templates/code/entity.ftl` | 实体类生成模板 | FreeMarker模板，用于生成JPA实体类代码 |
| `resources/templates/code/repository.ftl` | Repository生成模板 | FreeMarker模板，用于生成JPA Repository接口代码 |
| `resources/templates/code/service.ftl` | Service接口生成模板 | FreeMarker模板，用于生成Service接口代码 |
| `resources/templates/code/serviceImpl.ftl` | Service实现类生成模板 | FreeMarker模板，用于生成Service实现类代码 |
| `resources/templates/code/controller.ftl` | Controller生成模板 | FreeMarker模板，用于生成REST Controller代码 |

## 前端项目结构 (ui/)

### 配置文件
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `package.json` | NPM包管理配置 | 定义项目依赖、脚本命令、项目信息 |
| `vue.config.js` | Vue CLI配置 | 配置开发服务器代理、构建选项等 |
| `babel.config.js` | Babel编译配置 | 配置JavaScript编译选项 |
| `jsconfig.json` | JavaScript配置 | 配置路径映射、编辑器支持等 |

### 核心文件
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `src/main.js` | Vue应用入口文件 | 创建Vue应用实例，注册全局组件和插件 |
| `src/App.vue` | 根组件 | Vue应用的根组件，包含全局布局和路由出口 |

### API接口层 (src/api/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `src/api/index.js` | API接口统一导出 | 统一导出所有API接口，便于组件引用 |
| `src/api/request.js` | HTTP请求封装 | 封装axios，配置请求拦截器、响应拦截器 |
| `src/api/auth.js` | 用户认证API | 封装用户登录、注册、令牌验证等接口 |
| `src/api/codeGeneration.js` | 代码生成API | 封装代码生成任务、表配置、代码预览等接口 |
| `src/api/databaseConfig.js` | 数据库配置API | 封装数据库类型、字段类型配置等接口 |

### 组件库 (src/components/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `src/components/index.js` | 组件统一导出 | 统一导出所有可复用组件 |
| `src/components/CodeHighlight.vue` | 代码高亮组件 | 提供代码语法高亮显示和下载功能 |
| `src/components/EmptyState.vue` | 空状态组件 | 显示无数据状态的通用组件 |
| `src/components/HelloWorld.vue` | 示例组件 | Vue CLI生成的示例组件 |
| `src/components/LoadingWrapper.vue` | 加载状态包装组件 | 提供统一的加载状态显示 |
| `src/components/PageContainer.vue` | 页面容器组件 | 提供统一的页面布局容器 |

### 路由配置 (src/router/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `src/router/index.js` | Vue Router路由配置 | 配置应用的所有路由规则和导航守卫 |

### 页面视图 (src/views/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `src/views/LoginView.vue` | 登录页面 | 用户登录界面，包含登录表单和验证 |
| `src/views/LayoutView.vue` | 主布局页面 | 应用主体布局，包含侧边栏、顶部栏等 |
| `src/views/DashboardView.vue` | 仪表盘页面 | 首页仪表盘，显示系统概览信息 |
| `src/views/DatabaseConfig.vue` | 数据库配置页面 | 管理数据库类型和字段类型配置 |
| `src/views/CodeGeneration.vue` | 代码生成页面 | 核心功能页面，管理代码生成任务和流程 |

### 工具类 (src/utils/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `src/utils/index.js` | 通用工具函数 | 提供项目中常用的工具函数 |

### 静态资源 (src/assets/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `src/assets/logo.png` | 项目Logo图片 | 应用的标识图片 |

### 公共文件 (public/)
| 文件路径 | 功能说明 | 主要作用 |
|---------|---------|---------|
| `public/index.html` | HTML模板文件 | Vue应用的HTML模板，定义页面基本结构 |
| `public/favicon.ico` | 网站图标 | 浏览器标签页显示的小图标 |

## 核心功能模块详解

### 1. 用户认证模块
- **前端**: `LoginView.vue` + `auth.js`
- **后端**: `AuthController.java` + `UserService.java` + JWT安全组件
- **功能**: 用户注册、登录、JWT令牌管理、权限验证

### 2. 数据库配置模块
- **前端**: `DatabaseConfig.vue` + `databaseConfig.js`
- **后端**: `DatabaseConfigController.java` + `DatabaseConfigService.java`
- **功能**: 管理MySQL、SQLite、达梦三种数据库的字段类型配置

### 3. 代码生成核心模块
- **前端**: `CodeGeneration.vue` + `codeGeneration.js`
- **后端**: `CodeGenerationController.java` + `CodeGenerationService.java` + `CodeTemplateService.java`
- **功能**: 
  - 任务管理：创建、编辑、删除代码生成任务
  - 表结构设计：配置数据库表和字段
  - Repository生成：支持JPA查询方法定制
  - Service生成：支持方法选择和自然语言生成
  - 代码预览：实时预览生成的代码
  - 代码下载：支持单表和整体代码包下载

### 4. 模板引擎模块
- **模板文件**: `resources/templates/code/*.ftl`
- **服务**: `CodeTemplateService.java` + `FreemarkerConfig.java`
- **功能**: 基于FreeMarker的代码模板生成，支持实体类、Repository、Service、Controller等

### 5. JPA查询构建模块
- **服务**: `JpaQueryBuilderService.java`
- **功能**: 根据字段类型和条件自动生成JPA查询方法

## 技术栈说明

### 后端技术栈
- **Java 17**: 编程语言
- **Spring Boot 3.4**: 应用框架
- **Spring Data JPA**: 数据访问层
- **Spring Security**: 安全框架
- **JWT**: 身份认证
- **SQLite**: 嵌入式数据库
- **Redis**: 缓存存储
- **FreeMarker**: 模板引擎
- **Knife4j**: API文档
- **Maven**: 项目管理

### 前端技术栈
- **Vue 3**: 前端框架
- **Vue Router**: 路由管理
- **Element Plus**: UI组件库
- **Ant Design**: 补充UI组件
- **Axios**: HTTP客户端
- **NPM**: 包管理器

## 开发和维护建议

### 添加新功能时的注意事项
1. **后端**: 遵循MVC架构，先定义Entity和Repository，再实现Service和Controller
2. **前端**: 遵循组件化开发，将复用逻辑提取为组件
3. **API**: 保持RESTful风格，使用统一的响应格式
4. **模板**: 新增代码生成类型时，需要创建对应的FreeMarker模板

### 代码规范
1. **命名**: 使用有意义的类名、方法名和变量名
2. **注释**: 所有公共方法都需要详细的中文注释
3. **异常处理**: 统一的异常处理机制
4. **日志**: 关键操作需要记录日志

### 扩展建议
1. **数据库支持**: 可继续添加PostgreSQL、Oracle等数据库支持
2. **代码生成**: 可扩展生成移动端代码、微服务架构代码等
3. **AI集成**: 完善自然语言生成代码的功能
4. **版本管理**: 添加代码版本管理和回滚功能

## 联系信息

如需维护或扩展此项目，请参考此文档了解各文件的具体功能。建议在修改前仔细阅读相关代码和注释。