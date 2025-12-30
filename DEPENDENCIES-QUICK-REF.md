# 快速参考: PeerStreamEnterprise 依赖库清单

## 按字母顺序排列的完整库列表

| # | 库名 | 类型 | signal.js | execue.js | 说明 |
|---|------|------|----------|----------|------|
| 1 | @babel/preset-env | 开发 | ✅ | ✅ | Babel 预设配置 |
| 2 | axios | 网络 | ✅ | ✅ | HTTP 客户端库 |
| 3 | babel-loader | 开发 | ✅ | ✅ | Webpack Babel 加载器 |
| 4 | bcryptjs | 安全 | ✅ | ❌ | 密码加密库 |
| 5 | better-sqlite3 | 数据库 | ✅ | ❌ | 高性能 SQLite (可选) |
| 6 | chalk | 日志 | ✅ | ✅ | 控制台彩色输出 |
| 7 | child_process | 内置 | ✅ | ✅ | 进程管理 (Node.js 内置) |
| 8 | debug | 日志 | ✅ | ✅ | 调试工具 |
| 9 | fs | 内置 | ✅ | ✅ | 文件系统 (Node.js 内置) |
| 10 | glob | 工具 | ✅ | ❌ | 文件路径匹配 |
| 11 | https | 内置 | ✅ | ❌ | HTTPS 服务器 (Node.js 内置) |
| 12 | iconv-lite | 编码 | ✅ | ✅ | 字符编码转换 |
| 13 | jsonwebtoken | 安全 | ✅ | ✅ | JWT 认证 |
| 14 | keygrip | 安全 | ✅ | ✅ | 密钥签名 |
| 15 | koa | 框架 | ✅ | ❌ | Web 框架 |
| 16 | koa-bodyparser | 中间件 | ✅ | ❌ | 请求体解析 |
| 17 | koa-cors | 中间件 | ✅ | ❌ | 跨域支持 |
| 18 | koa-mount | 中间件 | ✅ | ❌ | 子应用挂载 |
| 19 | koa-router | 中间件 | ✅ | ❌ | 路由管理 |
| 20 | koa-static | 中间件 | ✅ | ❌ | 静态文件服务 |
| 21 | lodash | 工具 | ✅ | ✅ | 工具函数库 |
| 22 | lodash-es | 工具 | ✅ | ✅ | 工具函数库 (ES 模块) |
| 23 | node-gyp | 构建 | ✅ | ✅ | 原生模块构建 |
| 24 | os | 内置 | ✅ | ✅ | 系统信息 (Node.js 内置) |
| 25 | path | 内置 | ✅ | ✅ | 路径处理 (Node.js 内置) |
| 26 | sqlite3 | 数据库 | ✅ | ❌ | SQLite3 数据库 |
| 27 | systeminformation | 系统 | ✅ | ✅ | 系统监控库 |
| 28 | tls | 内置 | ✅ | ✅ | TLS 加密 (Node.js 内置) |
| 29 | webpack | 构建 | ✅ | ✅ | 模块打包器 |
| 30 | webpack-cli | 构建 | ✅ | ✅ | Webpack CLI 工具 |
| 31 | winston | 日志 | ✅ | ❌ | 日志框架 |
| 32 | ws | 网络 | ✅ | ✅ | WebSocket 库 |

## 库的分类统计

### 按类型分类
```
框架库:           5 个 (koa 系列)
网络通信:         3 个 (ws, axios, https/tls)
数据库:           2 个 (sqlite3, better-sqlite3)
安全认证:         3 个 (jsonwebtoken, bcryptjs, keygrip)
日志调试:         3 个 (chalk, debug, winston)
编码工具:         1 个 (iconv-lite)
工具函数:         2 个 (lodash, lodash-es)
系统监控:         1 个 (systeminformation)
构建工具:         4 个 (webpack, webpack-cli, babel-loader, node-gyp)
Node.js 内置:     7 个 (fs, path, os, child_process, https, tls)
```

### 按频率分类
```
两个文件都用:     18 个库 (核心库)
signal.js 独占:   14 个库 (API、数据库相关)
execue.js 独占:   0 个库
```

## 最小依赖集合

若要最小化部署，以下是必须的库：

```javascript
// 核心必需
const koa = require('koa');           // Web 框架
const Router = require('koa-router'); // 路由
const ws = require('ws');             // WebSocket
const axios = require('axios');       // HTTP
const iconv = require('iconv-lite');  // 编码
const jwt = require('jsonwebtoken');  // 认证
const sqlite3 = require('sqlite3');   // 数据库
const chalk = require('chalk');       // 日志
```

## 按包大小排序（估计）

| 库名 | 大小估计 | 说明 |
|------|---------|------|
| webpack | ~2-5 MB | 构建工具（仅开发） |
| better-sqlite3 | ~1-2 MB | 包含原生编译 |
| sqlite3 | ~1-2 MB | 数据库驱动 |
| babel-loader | ~1 MB | 构建工具（仅开发） |
| lodash | ~20-30 KB | 工具库 |
| axios | ~15-20 KB | HTTP 客户端 |
| ws | ~10-15 KB | WebSocket |
| koa | ~20-30 KB | Web 框架 |

## npm 安装命令

### 完整安装
```bash
npm install
```

### 按类型安装

**Web 框架**
```bash
npm install koa koa-router koa-bodyparser koa-static koa-cors
```

**网络通信**
```bash
npm install ws axios
```

**数据库**
```bash
npm install sqlite3
# 或高性能版本
npm install better-sqlite3
```

**安全认证**
```bash
npm install jsonwebtoken bcryptjs keygrip
```

**日志工具**
```bash
npm install chalk debug winston
```

**其他**
```bash
npm install lodash iconv-lite systeminformation
```

## 版本锁定建议

在 `package.json` 中使用的版本锁定策略：

```json
{
  "dependencies": {
    "koa": "^2.14.0",
    "ws": "^8.13.0",
    "axios": "^1.4.0",
    "sqlite3": "^5.1.6",
    "jsonwebtoken": "^9.0.0",
    "chalk": "^5.0.0",
    "lodash": "^4.17.21",
    "iconv-lite": "^0.6.3"
  },
  "devDependencies": {
    "webpack": "^5.80.0",
    "webpack-cli": "^5.0.0"
  }
}
```

## 常用命令

```bash
# 检查过期包
npm outdated

# 检查安全漏洞
npm audit

# 修复安全问题
npm audit fix

# 更新所有包到最新兼容版本
npm update

# 清理缓存
npm cache clean --force

# 打开包文档
npm home lodash
```

## 性能指标

### 包大小统计
- **signal.js 编译后**: ~65 KB (gzip)
- **execue.js 编译后**: ~61 KB (gzip)
- **合计**: ~126 KB (生产环境)

### 运行时内存占用
- **signal.js 进程**: ~50-100 MB (基础) + 缓存
- **execue.js 进程**: ~30-50 MB (基础) + UE 进程

### 编译时间
- **首次构建**: ~30-60 秒
- **增量构建**: ~5-10 秒

## 常见依赖冲突

### peer 依赖冲突
- `koa@2.x` 要求 `node >= 7.6`
- `ws@8.x` 支持 `node >= 10.x`
- `better-sqlite3` 需要原生编译（需要 C++ 工具链）

### 版本兼容性
```
Node.js 14.x:  ✅ 完全支持
Node.js 16.x:  ✅ 完全支持
Node.js 18.x:  ✅ 推荐
Node.js 20.x:  ✅ 推荐
```

## 安全更新注意事项

定期检查安全更新：
```bash
npm audit
npm audit fix

# 主要需要关注的库
npm outdated jsonwebtoken    # 安全认证
npm outdated bcryptjs        # 密码加密
npm outdated axios           # HTTP 请求
npm outdated ws              # WebSocket
```

## 更新日志（关键更新）

- **2024-09**: 添加 sqlite3 支持
- **2024-12**: 添加 WSS/HTTPS 支持
- **2025-01**: 优化 iconv-lite 字符处理
- **2025-05**: 完善 WebSocket 通信
- **2025-10**: UE5 像素流 V2 支持

