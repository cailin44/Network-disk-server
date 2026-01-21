
# WebDrive (Go 版) - 加密网盘系统

这是一个专为手机 APP 对接设计的跨平台加密网盘系统。采用 Go 语言编写，具备高性能、单文件分发和交互式管理控制台等特性。

## 🌟 核心特性

- **跨平台适配**：主动识别 Windows、Linux 和 macOS 系统，自动配置最佳存储路径。
- **端到端加密**：文件在服务器磁盘上采用 **AES-CTR** 模式加密存储，确保数据隐私。
- **APP 友好型 API**：基于 **Gin** 框架构建的 RESTful API，使用 **JWT** 进行身份验证。
- **交互式控制台**：服务器启动后保留控制台交互，支持实时指令管理（如动态添加用户、查看状态等）。
- **一键启动**：提供 Windows (.bat) 和 Linux/macOS (.sh) 启动脚本，自动编译运行。

## 🛠️ 技术架构

- **后端语言**: Js (JavaScript)
- **Web 框架**: Gin Gonic
- **认证机制**: JWT (JSON Web Token)
- **加密算法**: AES-256-CTR + SHA256 (密码哈希)
- **并发模型**: Goroutines (实现 API 服务与控制台交互并行)

## 🚀 快速启动

### 前提条件
- 已安装 [Go 环境](https://go.dev/dl/) (建议 1.18+)

### 启动步骤
1. **解压项目包**。
2. **运行启动脚本**：
   - **Windows**: 双击 `start.bat`
   - **Linux/macOS**: 执行 `chmod +x start.sh && ./start.sh`
3. **访问服务**：
   - API 地址: `http://localhost:8000`
   - 默认账号: `admin`
   - 默认密码: `admin123`

## 💻 控制台指令

服务器启动后，您可以在控制台输入以下指令进行实时管理：

| 指令 | 说明 | 示例 |
| :--- | :--- | :--- |
| `help` | 显示帮助信息 | `help` |
| `status` | 查看服务器运行状态及存储路径 | `status` |
| `list` | 列出服务器上存储的所有文件 | `list` |
| `users` | 列出当前所有授权用户 | `users` |
| `adduser` | 动态添加新用户（无需重启） | `adduser jack 123456` |
| `exit` | 安全关闭服务器并退出 | `exit` |

## 📱 APP 对接接口 (API)

| 接口 | 方法 | 说明 | 认证 |
| :--- | :--- | :--- | :--- |
| `/token` | POST | 登录获取 JWT Token | 否 |
| `/system/info` | GET | 获取服务器系统信息 | 是 |
| `/files` | GET | 获取文件列表 | 是 |
| `/upload` | POST | 加密上传文件 | 是 |
| `/download/:name` | GET | 解密下载文件 | 是 |
| `/delete/:name` | DELETE | 删除文件 | 是 |

## 🔒 安全说明
- 本项目默认使用内置密钥进行演示，**生产环境部署请务必修改 `security.go` 中的 `SecretKey` 和 `FileEncryptionKey`**。
- 建议在公网环境下配合 Nginx 使用 HTTPS 证书以保护传输层安全。
