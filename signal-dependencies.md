# signal.js 三方库依赖清单

## 项目概述
- **项目名**: PeerStreamEnterprise - 云渲染管理平台
- **类型**: Node.js + Webpack 打包应用
- **源文件**: signal.js（已编译打包）
- **配置文件**: signal.json
- **构建工具**: Webpack

---

## 核心依赖库

### 1. Web 框架和服务器
| 库名 | 版本 | 用途 | 来源 |
|-----|------|------|------|
| **koa** | - | 轻量级 Node.js Web 框架，用于 API 处理 | npm |
| **koa-router** | - | Koa 路由中间件 | npm |
| **koa-bodyparser** | - | Koa 请求体解析中间件 | npm |
| **koa-static** | - | Koa 静态文件服务中间件 | npm |
| **koa-cors** | - | Koa 跨域资源共享支持 | npm |

### 2. 数据库
| 库名 | 版本 | 用途 | 来源 |
|-----|------|------|------|
| **sqlite3** | - | 轻量级数据库，保存用户访问数据 | npm |
| **better-sqlite3** | - | 更快的 SQLite 驱动（可选）| npm |

### 3. 网络和通信
| 库名 | 版本 | 用途 | 来源 |
|-----|------|------|------|
| **ws** | - | WebSocket 实现 | npm |
| **axios** | - | HTTP 客户端库 | npm |

### 4. 编码和字符处理
| 库名 | 版本 | 用途 | 来源 |
|-----|------|------|------|
| **iconv-lite** | - | 字符编码转换（中文路径支持） | npm |

### 5. 安全相关
| 库名 | 版本 | 用途 | 来源 |
|-----|------|------|------|
| **keygrip** | - | 密钥签名库（Cookie 安全） | npm |
| **jsonwebtoken** | - | JWT token 生成和验证 | npm |

### 6. 日志和调试
| 库名 | 版本 | 用途 | 来源 |
|-----|------|------|------|
| **chalk** | - | 控制台彩色输出 | npm |
| **debug** | - | 调试工具库 | npm |

### 7. 工具函数库
| 库名 | 版本 | 用途 | 来源 |
|-----|------|------|------|
| **lodash** 或 **lodash-es** | - | 实用函数库 | npm |

---

## 从编译文件中检测到的依赖

### 直接检测到的模块
- `iconv-lite` - 在 webpack 打包中直接被引用（中文字符处理）
- `keygrip` - 安全密钥管理

### 隐含依赖
根据项目功能分析，以下库应该被使用：

#### 进程管理
- 内置 Node.js `child_process` 模块 - 用于启动/管理 UE 实例
- 内置 Node.js `os` 模块 - 用于获取 CPU、内存、GPU 信息
- 可能使用 `systeminformation` 库获取系统信息

#### 文件系统
- 内置 Node.js `fs` 和 `path` 模块
- 可能使用 `glob` 库进行文件匹配

---

## 项目使用的 API 端点所需库

根据 README 的功能更新记录：

| 功能 | 所需库 |
|-----|--------|
| API 处理框架 | koa, koa-router |
| 静态文件托管 | koa-static, koa-mount |
| 跨域支持 | koa-cors, koa2-cors |
| 认证鉴权 | jsonwebtoken, bcryptjs |
| 日志功能 | 内置或 winston |
| 数据库 | sqlite3 |
| 系统信息 | systeminformation 或内置 os 模块 |
| WebSocket | ws |
| HTTPS/WSS | 内置 https, 内置 tls |
| 配置管理 | 内置 JSON 解析 |

---

## 编译信息

### Webpack 配置
- **打包方式**: 单文件打包
- **输出**: signal.js（~65KB）、execue.js（~61KB）
- **许可证文件**: signal.js.LICENSE.txt、execue.js.LICENSE.txt

### 模块标识
从 webpack 编译中可以看出：
- 使用数字 ID 进行模块映射（如 `__webpack_modules__[64466]`）
- 支持动态 require（如 sqlite3 的动态加载）

---

## 安装/部署说明

该项目是已编译的形式，如果需要修改源代码，应该：

1. 查找原始 TypeScript 或 JavaScript 源文件
2. 查看 webpack.config.js 或 package.json
3. 通过 `npm install` 安装所有依赖
4. 通过 `npm run build` 或 `webpack` 重新编译

---

## 兼容性说明

### 支持的系统
- Windows（原生支持）
- Linux（优化兼容性）
- 国产信创环境（麒麟系统优化）

### 功能特性
- ✅ HTTPS/WSS 安全传输支持
- ✅ 多机器分布式部署
- ✅ UE4.27 及 UE5 支持
- ✅ 像素流 V2 版本支持
- ✅ GPU 负载均衡
- ✅ 自动路径寻路
- ✅ 坐标系转换

---

## 许可证信息

详见 signal.js.LICENSE.txt 和 execue.js.LICENSE.txt 文件

