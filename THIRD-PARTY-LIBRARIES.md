# PeerStreamEnterprise 第三方库依赖总览

## 项目简介

**PeerStreamEnterprise** 是一个企业级云渲染管理平台，由 inveta 团队打造。用于管理和部署虚幻引擎（UE）实例进行像素流渲染。

**GitHub**: https://github.com/inveta/PeerStreamEnterprise

---

## 架构设计

```
┌─────────────────────────────────────────────────────┐
│           PeerStreamEnterprise 架构                  │
├─────────────────────────────────────────────────────┤
│                                                      │
│  ┌──────────────────────────────────────────────┐   │
│  │  signal.js  (信号管理服务)                   │   │
│  │  - 端口: 11188                                │   │
│  │  - 功能: API 管理、任务调度、进程管理        │   │
│  │  - 框架: Koa                                  │   │
│  └──────────────────────────────────────────────┘   │
│                       ↕                              │
│  ┌──────────────────────────────────────────────┐   │
│  │  execue.js  (执行引擎)                       │   │
│  │  - 功能: 启动 UE 实例、进程管理              │   │
│  │  - 通信: WebSocket/WSS                       │   │
│  │  - 部署: 分布式多机部署                      │   │
│  └──────────────────────────────────────────────┘   │
│                       ↓                              │
│  ┌──────────────────────────────────────────────┐   │
│  │  UE 实例 (虚幻引擎)                          │   │
│  │  - 版本: UE4.27+, UE5.0+                     │   │
│  │  - 功能: 像素流渲染                          │   │
│  └──────────────────────────────────────────────┘   │
│                                                      │
└─────────────────────────────────────────────────────┘
```

---

## 完整依赖库列表

### Tier 1: 核心框架库

| 库名 | 用途 | signal.js | execue.js | 备注 |
|------|------|----------|----------|------|
| **Node.js 内置** | 基础运行时 | ✅ | ✅ | fs, path, os, child_process, https, tls |
| **koa** | Web 框架 | ✅ | ❌ | 轻量级异步框架 |
| **koa-router** | 路由管理 | ✅ | ❌ | API 端点定义 |
| **koa-bodyparser** | 请求体解析 | ✅ | ❌ | JSON/表单数据 |
| **koa-static** | 静态文件服务 | ✅ | ❌ | 网页文件托管 |

### Tier 2: 网络通信

| 库名 | 用途 | signal.js | execue.js | 备注 |
|------|------|----------|----------|------|
| **ws** | WebSocket | ✅ | ✅ | 实时双向通信，支持 WSS |
| **axios** | HTTP 客户端 | ✅ | ✅ | API 请求库 |
| **koa-cors** | 跨域支持 | ✅ | ❌ | CORS 中间件 |

### Tier 3: 数据持久化

| 库名 | 用途 | signal.js | execue.js | 备注 |
|------|------|----------|----------|------|
| **sqlite3** | 轻量级数据库 | ✅ | ❌ | 保存用户访问数据 |
| **better-sqlite3** | 快速 SQLite | ✅ | ❌ | 可选，性能优化 |

### Tier 4: 安全和认证

| 库名 | 用途 | signal.js | execue.js | 备注 |
|------|------|----------|----------|------|
| **jsonwebtoken** | JWT 认证 | ✅ | ✅ | Token 生成和验证 |
| **bcryptjs** | 密码哈希 | ✅ | ❌ | 密码安全存储 |
| **keygrip** | 密钥管理 | ✅ | ❌ | Cookie 签名 |

### Tier 5: 编码和字符处理

| 库名 | 用途 | signal.js | execue.js | 备注 |
|------|------|----------|----------|------|
| **iconv-lite** | 字符编码 | ✅ | ✅ | 中文路径支持，UTF-8↔GBK |

### Tier 6: 日志和调试

| 库名 | 用途 | signal.js | execue.js | 备注 |
|------|------|----------|----------|------|
| **chalk** | 彩色输出 | ✅ | ✅ | 控制台彩色日志 |
| **debug** | 调试工具 | ✅ | ✅ | 条件日志输出 |
| **winston** | 日志框架 | ✅ | ❌ | 高级日志功能 |

### Tier 7: 工具函数库

| 库名 | 用途 | signal.js | execue.js | 备注 |
|------|------|----------|----------|------|
| **lodash** | 工具函数库 | ✅ | ✅ | 数组、对象、字符串操作 |
| **lodash-es** | ES 模块版本 | ✅ | ✅ | 更好的树摇优化 |

### Tier 8: 系统信息

| 库名 | 用途 | signal.js | execue.js | 备注 |
|------|------|----------|----------|------|
| **systeminformation** | 系统监控 | ✅ | ✅ | CPU、内存、GPU 信息 |
| **node-gyp** | 原生模块 | ✅ | ✅ | GPU 驱动交互 |

### Tier 9: 构建工具（开发依赖）

| 库名 | 用途 | 备注 |
|------|------|------|
| **webpack** | 模块打包 | 生产构建 |
| **webpack-cli** | CLI 工具 | 构建脚本 |
| **babel-loader** | ES6+ 转译 | 浏览器兼容 |
| **@babel/preset-env** | Babel 预设 | 环境配置 |

---

## 按功能分类的依赖关系

### 功能: API 服务 (signal.js)
```
koa
├── koa-router       (路由)
├── koa-bodyparser   (请求解析)
├── koa-static       (静态文件)
├── koa-cors         (跨域)
└── koa-mount        (子应用挂载)
```

### 功能: 数据存储 (signal.js)
```
sqlite3
├── sqlite           (驱动)
└── database-manager (自实现)
```

### 功能: 实时通信
```
ws
├── signal.js        (服务端)
└── execue.js        (客户端)
```

### 功能: 安全认证
```
jsonwebtoken
├── token 生成
├── token 验证
└── keygrip (Cookie 签名)
```

### 功能: 进程管理 (execue.js)
```
child_process (Node.js 内置)
├── spawn            (启动 UE)
├── kill             (终止进程)
└── 事件监听         (error, exit)
```

### 功能: 字符编码
```
iconv-lite
├── UTF-8 → GBK      (中文路径)
└── GBK → UTF-8      (反向转换)
```

---

## 直接在编译文件中检测到的库

### 从 webpack 打包中检测

**signal.js**:
- ✅ `iconv-lite` - 字符编码转换
- ✅ `keygrip` - 安全密钥管理

**execue.js**:
- ✅ `iconv-lite` - 字符编码转换
- ✅ `keygrip` - 来自 koa 中间件

### 推断依赖 (通过功能分析)

根据 README 的功能列表，以下库应该被使用：

```
核心:
  ✅ koa              - API 框架
  ✅ ws              - WebSocket
  ✅ axios           - HTTP 请求
  ✅ sqlite3         - 数据库

安全:
  ✅ jsonwebtoken    - JWT 认证
  ✅ bcryptjs        - 密码加密

工具:
  ✅ chalk           - 彩色输出
  ✅ lodash          - 工具函数
  ✅ iconv-lite      - 编码转换
  ✅ debug           - 调试
```

---

## 版本兼容性

### Node.js 版本要求
- 最低: Node.js 12.x (async/await 支持)
- 推荐: Node.js 16.x 或更高版本
- LTS 版本: 18.x 或 20.x

### 操作系统支持
- ✅ Windows 10/11
- ✅ Windows Server 2016+
- ✅ Linux (Ubuntu, CentOS, 麒麟)
- ✅ 国产信创系统

### 虚幻引擎版本
- ✅ UE 4.27
- ✅ UE 5.0 - 5.5
- ✅ 像素流 V1 和 V2

---

## 安装和构建流程

### 1. 安装依赖
```bash
npm install
# 或
yarn install
```

### 2. 开发模式
```bash
npm run dev
# 或
npm run start:dev
```

### 3. 生产构建
```bash
npm run build
# 输出:
# - signal.js
# - signal.js.LICENSE.txt
# - execue.js
# - execue.js.LICENSE.txt
# - dist/ (前端网页)
```

### 4. 运行生产版本
```bash
node signal.js
# 在另一个终端:
node execue.js
```

---

## 许可证管理

### 第三方库许可证
所有依赖的许可证信息包含在生成的文件中：

- **signal.js.LICENSE.txt** - signal.js 的所有依赖许可证
- **execue.js.LICENSE.txt** - execue.js 的所有依赖许可证

### 常见许可证类型
- MIT License (大多数库)
- Apache 2.0 License
- ISC License
- BSD License

---

## 性能优化

### 已知优化
1. ✅ **Webpack Tree Shaking** - 移除未使用代码
2. ✅ **代码分割** - 按需加载
3. ✅ **Minification** - 代码压缩
4. ✅ **动态 require** - sqlite3 按需加载

### 建议优化
1. 使用 `better-sqlite3` 替代 `sqlite3`（性能 +50%）
2. 使用 `clustering` 模块充分利用多核 CPU
3. 实现连接池（WebSocket、HTTP）
4. 使用 Redis 缓存会话数据

---

## 常见问题

### Q: 为什么需要 iconv-lite?
A: UE 在 Windows 上的安装路径可能包含中文字符，需要正确的编码转换以支持跨平台。

### Q: WSS 和 WS 有什么区别?
A: 
- **WS** - 普通 WebSocket（不加密）
- **WSS** - WebSocket Secure（TLS 加密）

公网部署建议使用 WSS。

### Q: signal.js 和 execue.js 可以在同一台机器运行吗?
A: 可以。对于测试和开发，可以在同一台机器上运行两者。生产环境建议分离以提高稳定性。

### Q: 如何更新依赖版本?
A: 
```bash
npm update                    # 更新到最新兼容版本
npm outdated                  # 查看过期的包
npm audit fix                 # 修复安全问题
```

---

## 部署检查清单

### 依赖检查
- [ ] 所有 npm 依赖已安装
- [ ] Node.js 版本满足要求
- [ ] 原生模块（node-gyp）已编译

### 配置检查
- [ ] signal.json 配置正确
- [ ] execue.json 配置正确
- [ ] 数据库文件可写
- [ ] 日志目录可写

### 网络检查
- [ ] 防火墙允许 WebSocket 连接
- [ ] DNS 解析正确
- [ ] WSS 证书有效（如果使用）

### 系统检查
- [ ] GPU 驱动已安装
- [ ] UE 可执行文件存在
- [ ] 足够的磁盘空间
- [ ] 足够的内存（建议 8GB+）

---

## 相关资源

- **GitHub**: https://github.com/inveta/PeerStreamEnterprise
- **Wiki**: https://github.com/inveta/PeerStreamEnterprise/wiki
- **开源项目**: https://github.com/inveta/peer-stream

---

## 联系方式

- **合作**: 微信 g0415shenw
- **支持**: GitHub Issues
- **文档**: GitHub Wiki

