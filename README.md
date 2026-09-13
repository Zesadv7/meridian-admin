<h1 align="center">
    <img alt="logo" src="./meridian-frontend/src/assets/logo/logo.png">
</h1>
<h1 align="center" style="margin: 30px 0 30px; font-weight: bold;">Meridian Admin</h1>
<h4 align="center">前后端分离的企业级中后台权限管理系统</h4>

## 项目简介

Meridian 是一套前后端分离的中后台权限管理系统:后端基于 FastAPI + SQLAlchemy 2.0 全异步栈,前端基于 Vue3 + Element Plus。内置完整的用户-角色-菜单 RBAC 权限体系、JWT 多终端认证、数据权限、操作/登录日志审计、在线可视化定时任务、代码生成器、文件管理与插件系统,开箱即用。

## 技术栈

| 层 | 技术 |
|---|---|
| 后端框架 | FastAPI + Uvicorn(全异步 ASGI) |
| ORM / 数据库 | SQLAlchemy 2.0(AsyncSession,驱动 asyncmy / asyncpg) + MySQL / PostgreSQL |
| 缓存 | Redis(asyncio 客户端,会话/字典/参数/限流/日志队列) |
| 认证 | OAuth2 + JWT(PyJWT,HS256)+ bcrypt 密码哈希 |
| 定时任务 | APScheduler(数据库为配置源,多实例 Leader 选举) |
| 日志 | Loguru + Redis Stream 异步聚合 |
| 前端 | Vue 3 + Vite + Element Plus + Pinia + Vue Router |
| 部署 | Docker Compose(前端 nginx / 后端 / MySQL / Redis 四容器) |

## 核心功能

- **权限管理**:用户、角色、菜单、部门、岗位五维 RBAC;接口级 + 按钮级 + 数据权限(全部/自定义/本部门/本部门及以下/仅本人)
- **认证安全**:OAuth2 + JWT 多终端认证、图形验证码、账号锁定、IP 黑名单、传输层信封加密(RSA-OAEP + AES-256-GCM)
- **系统监控**:在线用户、服务监控(CPU/内存/磁盘)、缓存监控、操作日志、登录日志
- **任务调度**:可视化定时任务,在线增删改,支持 cron 表达式与执行日志
- **开发提效**:代码生成器(读表结构一键生成前后端 CRUD 代码)、在线表单构建
- **文件中心**:文件上传下载、访问控制(ACL)、回收站、保留策略与对账审计
- **插件系统**:插件热插拔(含内置 AI 对话插件,支持多模型管理)
- **移动端**:uni-app 移动端(可选)

## 快速开始(Docker)

```bash
docker compose -f docker-compose.my.yml up -d --build
```

启动完成后访问 <http://localhost:12580>,默认账号:

| 账号 | 密码 |
|---|---|
| admin | admin123 |

四个服务:前端(12580)、后端(19099→9099)、MySQL(13306,库 `meridian_admin`,首次启动自动执行建表脚本)、Redis(16379)。

## 本地开发

### 前端

```bash
cd meridian-frontend
npm install
npm run dev
```

### 后端

```bash
cd meridian-backend
pip3 install -r requirements.txt
# 1. 编辑 .env.dev 配置数据库与 Redis 连接
# 2. 新建数据库 meridian_admin,执行 sql/meridian_admin.sql
meridian app run --env=dev
```

生产环境使用 `.env.prod` 与 `meridian app run --env=prod`;PostgreSQL 版使用 `requirements-pg.txt` 与 `sql/meridian_admin_pg.sql`。

## 目录结构

```
meridian-admin
├── meridian-backend     # FastAPI 后端(SQL 脚本在 sql/ 目录)
├── meridian-frontend    # Vue3 管理端前端
├── meridian-app         # uni-app 移动端(可选)
└── meridian-test        # Playwright 端到端测试套件
```

## License

本项目基于 MIT 协议开源。
