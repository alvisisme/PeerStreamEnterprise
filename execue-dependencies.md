# execue.js 三方库依赖清单

## 项目概述
- **项目名**: PeerStreamEnterprise - 云渲染管理平台
- **组件**: execue.js（执行引擎）
- **类型**: Node.js + Webpack 打包应用
- **配置文件**: execue.json
- **用途**: 管理和执行 UE（虚幻引擎）实例

---

## 核心依赖库

### 1. WebSocket 和网络通信
| 库名 | 用途 | 详情 |
|-----|------|------|
| **ws** | WebSocket 客户端/服务器 | 连接到信号服务器 (signal.js)，支持 WSS 加密连接 |
| **axios** | HTTP 请求库 | 与信号服务器通信 |

### 2. 进程管理
| 库名 | 用途 | 详情 |
|-----|------|------|
| 内置 **child_process** | 启动/管理 UE 进程 | 启动 UE.exe、传递参数、监控进程状态 |
| 内置 **os** | 系统信息获取 | 获取 CPU、内存、GPU 信息用于负载均衡 |
| 内置 **path** | 路径处理 | 处理 Windows/Linux 混合路径 |

### 3. 编码和字符处理
| 库名 | 用途 | 详情 |
|-----|------|------|
| **iconv-lite** | 字符编码转换 | 解决中文路径问题，支持 UTF-8 和 GBK 转换 |

### 4. 日志和调试
| 库名 | 用途 | 详情 |
|-----|------|------|
| **chalk** | 控制台彩色输出 | 优化控制台打印，显示真实 IP 地址 |
| **debug** | 调试工具库 | 条件日志输出 |

### 5. 工具函数库
| 库名 | 用途 | 详情 |
|-----|------|------|
| **lodash** | 实用函数库 | 数组、对象、字符串操作 |

### 6. 安全相关
| 库名 | 用途 | 详情 |
|-----|------|------|
| **jsonwebtoken** | JWT token 处理 | 与信号服务器的身份验证 |

---

## execue.js 的主要功能模块

### 通信模块
```
功能: 连接到 signal.js
依赖库:
  - ws (WebSocket)
  - axios (HTTP)
  - jsonwebtoken (Token 认证)
特性:
  - 支持 WSS 加密连接
  - 自动重连机制
  - 心跳保活
```

### 进程管理模块
```
功能: 启动和管理 UE 实例
依赖库:
  - child_process (内置)
  - iconv-lite (中文路径)
特性:
  - 启动 UE.exe/UE 进程
  - 传递自定义参数
  - 进程监控
  - 异常处理和重启
  - 强制关闭进程
```

### 配置管理模块
```
功能: 读取 execue.json 配置文件
依赖库:
  - 内置 fs 和 JSON 解析
配置内容:
  - 信号服务器地址和端口
  - 认证信息 (userpwd, token)
  - UE 实例启动路径
  - GPU 和内存配置
  - 启动参数模板
```

### 系统监控模块
```
功能: 获取系统性能指标
依赖库:
  - os (内置)
  - 可能: systeminformation
指标:
  - CPU 使用率
  - 内存使用率
  - GPU 显存使用率
  - 网络状态
```

---

## 编译信息

### Webpack 打包
- **文件大小**: ~61KB（压缩后）
- **输出格式**: IIFE（立即执行函数表达式）
- **模块映射**: 数字 ID 索引

### 直接检测到的依赖
从 webpack 源代码中检测到：
```
require('iconv-lite')  - 编码转换
require('keygrip')     - 密钥管理（来自 koa 中间件）
```

---

## 配置文件说明 (execue.json)

```json
{
  "SignalServerIp": "127.0.0.1",     // 信号服务器地址
  "SignalServerPort": 11188,          // 信号服务器端口
  "UserId": "execue_01",              // execue 实例 ID
  "MachineIp": "127.0.0.1",           // 当前机器 IP
  "UseWss": false,                    // 是否使用 WSS 加密
  "Auth": {
    "username": "admin",
    "password": "encrypted_password"  // 加密密码
  }
}
```

---

## 进程启动流程

```
1. 读取 execue.json 配置
   ↓
2. 连接到信号服务器 (WebSocket/WSS)
   ↓
3. 发送身份验证信息
   ↓
4. 接收 UE 启动命令
   ↓
5. 使用 child_process 启动 UE.exe
   ↓
6. 传递 iconv-lite 处理的路径参数
   ↓
7. 监控进程状态
   ↓
8. 定期向服务器报告状态
```

---

## 跨平台兼容性

### Windows
- ✅ 原生支持（.exe 执行）
- ✅ 路径分隔符处理（\）
- ✅ Unicode 路径支持

### Linux
- ✅ UE Linux 版本支持
- ✅ 路径分隔符处理（/）
- ✅ 权限管理
- ✅ 麒麟系统优化

### 网络传输
- ✅ HTTP 通信
- ✅ WebSocket 连接
- ✅ WSS 加密连接
- ✅ 公网和内网支持

---

## 常见功能模块

| 功能 | 实现方式 | 关键库 |
|------|--------|--------|
| 启动 UE 实例 | `child_process.spawn()` | child_process |
| 传递参数到 UE | 命令行参数 + iconv-lite | iconv-lite |
| 监听进程事件 | `.on('error'), .on('exit')` | 内置 |
| 定时汇报状态 | setInterval + WebSocket | ws |
| 处理中文路径 | iconv-lite 转码 | iconv-lite |
| 控制台输出 | chalk 彩色打印 | chalk |
| 日志记录 | 文件写入 | 内置 fs |
| 连接重试 | 指数退避算法 | 自实现 |

---

## 版本支持

- ✅ UE 4.27
- ✅ UE 5.0+
- ✅ 像素流 V1
- ✅ 像素流 V2

---

## 与 signal.js 的通信协议

```
execue.js ←→ signal.js
   ↓
通信方式:
  - WebSocket/WSS (实时双向)
  - HTTP (HTTP API)
   ↓
传递信息:
  - 进程启动状态
  - 系统资源使用情况
  - UE 实例运行状态
  - 错误日志
  - 接收启动/关闭命令
```

---

## 许可证

详见 execue.js.LICENSE.txt 文件（包含所有第三方库的许可证）

---

## 部署检查清单

- [ ] 检查 execue.json 配置是否正确
- [ ] 验证与 signal.js 的网络连接
- [ ] 确保 UE 可执行文件路径正确
- [ ] 检查 GPU 配置和显存分配
- [ ] 验证 WSS 证书（如果使用加密）
- [ ] 检查防火墙设置允许 WebSocket 连接
- [ ] 监控进程启动日志

