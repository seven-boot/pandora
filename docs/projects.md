## 创建项目组

按照下列顺序创建即可

- pandora-denpendencies：通用依赖版本控制：依赖于一个二方库群时，必须定义一个统一的版本变量，避免版本号不一致
- pandora-parent：通用父工程：产品线下的所有项目必须指定一个父工程项目，以复用 `<build>` 配置
- pandora-commons：通用的工具类库
- pandora-generator：通用代码生成器：如 Mybatis Plus
- pandora-oauth：认证与授权：独立的认证与授权服务
- pandora-cloud：外部接口或第三方平台：包括其他部门 RPC 开放接口，基础平台，其他公司的 HTTP 接口
- docs：用于存放项目文档的目录