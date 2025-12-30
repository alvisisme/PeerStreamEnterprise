# 📚 PeerStreamEnterprise 第三方库依赖文档

## 📋 文档概览

本目录包含 PeerStreamEnterprise 项目的完整第三方库依赖分析和文档。

### 📄 已生成的文档文件

| 文档文件 | 说明 | 适用场景 |
|---------|------|---------|
| **THIRD-PARTY-LIBRARIES.md** | 完整的依赖库总览 | 全面了解项目架构和依赖关系 |
| **signal-dependencies.md** | signal.js 专项分析 | 研究信号管理服务 |
| **execue-dependencies.md** | execue.js 专项分析 | 研究 UE 执行引擎 |
| **DEPENDENCIES-QUICK-REF.md** | 快速参考表 | 快速查询和部署 |
| **README.md** (原有) | 项目简介 | 了解项目全貌 |
| **signal.json** (原有) | signal 配置示例 | 配置参考 |
| **execue.json** (原有) | execue 配置示例 | 配置参考 |

---

## 🎯 快速导航

### 我想...

#### 📖 了解整个项目的架构和依赖
→ 阅读 **THIRD-PARTY-LIBRARIES.md**

**包含内容:**
- 项目整体架构图
- 完整依赖库列表（32+ 个库）
- 按功能分类的依赖关系
- 架构设计说明

#### 🔍 只想看 signal.js (信号管理服务) 的依赖
→ 阅读 **signal-dependencies.md**

**包含内容:**
- Web 框架 (Koa)
- API 路由和中间件
- 数据库 (SQLite3)
- 认证和安全
- 静态文件服务

#### ⚙️ 只想看 execue.js (UE 执行引擎) 的依赖
→ 阅读 **execue-dependencies.md**

**包含内容:**
- WebSocket 通信
- 进程管理
- 字符编码处理
- 系统监控
- 进程启动流程

#### 📊 快速查看依赖库列表和版本
→ 阅读 **DEPENDENCIES-QUICK-REF.md**

**包含内容:**
- 按字母顺序的完整列表
- 包大小统计
- npm 安装命令
- 版本推荐
- 常见命令集合

#### 🚀 快速部署或开发
→ 查看 **快速部署检查清单** (见下方)

#### 🔐 了解安全和认证
→ 在 THIRD-PARTY-LIBRARIES.md 中查看 **Tier 4: 安全和认证** 部分

---

## 📦 依赖库统计

```
总库数:              32+ 个
核心库:              18 个 (两个文件都用)
signal.js 独占:      14 个
Node.js 内置:        7 个
开发依赖:            4 个
```

### 最常用的 TOP 10 库

1. **koa** - Web 框架
2. **ws** - WebSocket 通信
3. **axios** - HTTP 客户端
4. **sqlite3** - 数据库
5. **jsonwebtoken** - JWT 认证
6. **iconv-lite** - 字符编码
7. **chalk** - 彩色日志
8. **lodash** - 工具函数
9. **child_process** - 进程管理
10. **fs/path** - 文件系统

---

## 🔑 核心依赖速览

### Web API 层 (signal.js)
```
Koa Web Framework
├── 路由: koa-router
├── 请求解析: koa-bodyparser
├── 静态文件: koa-static
├── 跨域: koa-cors
└── 端口: 11188
```

### 通信层
```
WebSocket Communication
├── 服务端: signal.js (ws 库)
├── 客户端: execue.js (ws 库)
├── HTTP: axios 库
└── 加密: WSS/TLS 支持
```

### 数据层 (signal.js)
```
SQLite3 Database
├── 存储: 用户访问数据
├── 驱动: sqlite3 或 better-sqlite3
└── 文件: *.db
```

### 认证层
```
Security & Auth
├── JWT: jsonwebtoken
├── Password: bcryptjs
├── Key Signing: keygrip
└── API Token: 自实现
```

### 进程管理层 (execue.js)
```
Process Management
├── 启动 UE: child_process
├── 监控: os 模块
├── 字符编码: iconv-lite
└── 通信: ws + axios
```

---

## 🛠️ 快速部署检查清单

### 前置条件
- [ ] Node.js 16.x 或更高版本 (推荐 18.x/20.x)
- [ ] npm 或 yarn 包管理器
- [ ] 足够的磁盘空间 (~500MB)
- [ ] 管理员权限 (Windows)

### 依赖检查
```bash
# 1. 安装所有依赖
npm install

# 2. 检查依赖是否完整
npm ls --depth=0

# 3. 检查安全问题
npm audit

# 4. 修复已知问题
npm audit fix
```

### 构建步骤
```bash
# 1. 开发调试构建
npm run dev

# 2. 生产构建
npm run build

# 3. 输出文件
ls -la signal.js execue.js
```

### 运行服务
```bash
# 终端 1: 运行信号管理服务
node signal.js

# 终端 2: 运行 UE 执行引擎
node execue.js
```

### 验证部署
```bash
# 检查信号服务是否运行
curl http://127.0.0.1:11188/api/health

# 检查日志
tail -f logs/signal.log
tail -f logs/execue.log
```

---

## 📝 配置文件示例

### signal.json 核心配置
```json
{
  "PORT": 11188,
  "auth": true,
  "userpwd": "admin:hash",
  "iceServers": [{"urls": ["stun:stun.l.google.com:19302"]}],
  "globlesetting": {
    "WebRTCMaxBitrate": 25,
    "WebRTCFps": 30,
    "ResX": 1920,
    "ResY": 1080
  }
}
```

### execue.json 核心配置
```json
{
  "SignalServerIp": "127.0.0.1",
  "SignalServerPort": 11188,
  "UserId": "execue_01",
  "UseWss": false
}
```

---

## 🌐 网络要求

### 端口配置
```
Signal 服务:
  ├── HTTP: 11188
  ├── WebSocket: 11188
  └── HTTPS/WSS: 可配置

UE 实例:
  ├── 像素流: 8888-8900
  ├── 信号通信: 11188
  └── RTC: 动态分配
```

### 防火墙规则
```
入站:
  ✅ TCP 11188 (Signal API)
  ✅ WebSocket 11188 (Real-time)
  ✅ TCP 8888-8900 (Pixel Stream)

出站:
  ✅ UDP 3478-3479 (STUN/TURN)
  ✅ 自定义 STUN 服务器
```

---

## 🔒 安全最佳实践

### 认证配置
```javascript
// JWT Token 配置
const tokenConfig = {
  algorithm: 'HS256',
  expiresIn: '24h',
  issuer: 'inveta'
};

// 密码加密
const bcryptRounds = 10;
```

### HTTPS/WSS 配置
```javascript
// 生产环境推荐配置
{
  ssl: true,
  cert: '/path/to/cert.pem',
  key: '/path/to/key.pem',
  protocol: 'wss://'
}
```

### 安全头部
```javascript
// API 响应头
headers: {
  'X-Content-Type-Options': 'nosniff',
  'X-Frame-Options': 'DENY',
  'X-XSS-Protection': '1; mode=block',
  'Strict-Transport-Security': 'max-age=31536000'
}
```

---

## 📊 性能指标

### 编译输出
```
signal.js:        ~65 KB (gzip)
execue.js:        ~61 KB (gzip)
合计:              ~126 KB
```

### 运行时占用
```
signal.js:        50-150 MB (含缓存)
execue.js:        30-80 MB + UE 进程
```

### 响应时间
```
API 响应:          < 100ms
WebSocket 连接:    < 500ms
UE 启动:           5-30秒
```

---

## 🆘 常见问题解决

### 问题 1: 中文路径错误
**症状**: 启动 UE 失败，路径乱码
**解决**: 检查 iconv-lite 库是否正确安装
```bash
npm rebuild iconv-lite
```

### 问题 2: WebSocket 连接失败
**症状**: execue 无法连接到 signal
**解决**: 检查防火墙和网络配置
```bash
# Windows
netstat -an | findstr 11188

# Linux
netstat -an | grep 11188
```

### 问题 3: SQLite3 编译错误
**症状**: npm install 时 sqlite3 编译失败
**解决**: 使用 better-sqlite3 或安装构建工具
```bash
# Windows 需要 Visual Studio Build Tools
npm install --build-from-source sqlite3

# 或使用更快的驱动
npm install better-sqlite3
```

### 问题 4: 高 CPU/内存 占用
**症状**: signal 或 execue 进程占用资源过多
**解决**: 
- 检查 WebSocket 连接数
- 调整数据库查询
- 启用 clustering 模块分散负载

---

## 📚 相关资源链接

### 官方文档
- [PeerStreamEnterprise GitHub](https://github.com/inveta/PeerStreamEnterprise)
- [项目 Wiki](https://github.com/inveta/PeerStreamEnterprise/wiki)
- [开源项目 peer-stream](https://github.com/inveta/peer-stream)

### 依赖库文档
- [Koa.js](https://koajs.com/)
- [ws 库](https://github.com/websockets/ws)
- [axios](https://axios-http.com/)
- [sqlite3](https://github.com/TryGhost/node-sqlite3)
- [jsonwebtoken](https://github.com/auth0/node-jsonwebtoken)

### 虚幻引擎文档
- [Pixel Streaming 文档](https://docs.unrealengine.com/5.0/en-US/pixel-streaming-in-unreal-engine/)
- [UE4.27 像素流](https://docs.unrealengine.com/4.27/en-US/SharingAndReleasing/PixelStreaming/)
- [UE5 像素流 V2](https://docs.unrealengine.com/5.0/en-US/pixel-streaming-in-unreal-engine/)

---

## 📞 技术支持

### 获取帮助
- 微信: g0415shenw (合作咨询)
- GitHub Issues: 提交问题报告
- GitHub Discussions: 技术讨论

### 反馈和建议
- 创建 GitHub Issue
- 提交 Pull Request
- 在 Wiki 上分享经验

---

## 📄 文档版本

- **版本**: 1.0
- **更新日期**: 2025年
- **适用范围**: PeerStreamEnterprise
- **维护者**: 自动分析工具

---

## 📌 使用指南总结

### 快速开始 (5 分钟)
1. `npm install` - 安装依赖
2. 编辑 `signal.json` 和 `execue.json` - 配置参数
3. `npm run build` - 构建项目
4. `node signal.js` + `node execue.js` - 启动服务

### 深入学习 (30 分钟)
1. 阅读 **THIRD-PARTY-LIBRARIES.md** - 了解架构
2. 阅读 **signal-dependencies.md** - 学习 API 层
3. 阅读 **execue-dependencies.md** - 学习进程管理

### 生产部署 (1 小时)
1. 检查部署清单
2. 配置 HTTPS/WSS
3. 设置数据库备份
4. 配置监控和日志
5. 进行压力测试

---

**祝您使用愉快！🚀**

如有问题，请参考相应的文档或提交 GitHub Issue。

