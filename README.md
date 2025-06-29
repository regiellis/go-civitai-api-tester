# Civitai API Tester 🧪

![Go Version](https://img.shields.io/badge/Go-1.21+-00ADD8?logo=go&logoColor=white)
![Minimal Dependencies](https://img.shields.io/badge/Dependencies-Minimal-00D084?logo=go&logoColor=white)
![Real-time Updates](https://img.shields.io/badge/WebSocket-Real--time-4CAF50?logo=socket.io&logoColor=white)
![Cross Platform](https://img.shields.io/badge/Platform-Cross--Platform-blue?logo=github&logoColor=white)
![Security Warning](https://img.shields.io/badge/⚠️-DEV%20TOOL%20ONLY-red?logo=security&logoColor=white)

---

>[!WARNING]
> **🚨 DEVELOPMENT TOOL ONLY!** This is a testing and development tool that should **NEVER** be exposed to public networks or used in production environments. Keep it local and secure! 🔒

>[!TIP]
> **Minimal Dependencies Magic!** ✨ This tester uses **only one external dependency** (gorilla/websocket for real-time updates) plus Go's standard library. No complex dependency trees, no version conflicts, no headaches!

>[!IMPORTANT]
> **Complete API Coverage!** 🚀 Tests every major CivitAI API endpoint with detailed reporting, performance metrics, and beautiful WebSocket-powered real-time dashboard. Perfect for SDK development, API monitoring, and integration testing.

---



### Download Pre-built Binary

>[!NOTE]
> **Automatic Releases:** Every tagged version automatically builds for all platforms via GitHub Actions! 🤖

Download the appropriate binary for your platform from the [releases section](../../releases):

| Platform | Download | Notes |
|----------|----------|-------|
| 🐧 **Linux (x64)** | `civitai-tester-linux-amd64.tar.gz` | Most common Linux systems |
| 🐧 **Linux (ARM64)** | `civitai-tester-linux-arm64.tar.gz` | Raspberry Pi, Apple Silicon Linux |
| 🪟 **Windows (x64)** | `civitai-tester-windows-amd64.zip` | Windows 10/11 |
| 🪟 **Windows (ARM64)** | `civitai-tester-windows-arm64.zip` | Surface Pro X, ARM Windows |
| 🍎 **macOS (Intel)** | `civitai-tester-darwin-amd64.tar.gz` | Intel-based Macs |
| 🍎 **macOS (Apple Silicon)** | `civitai-tester-darwin-arm64.tar.gz` | M1/M2/M3 Macs |

### Hello, API Testing! 👋

```bash
# Extract and run (macOS/Linux)
tar -xzf civitai-tester-linux-amd64.tar.gz
chmod +x civitai-tester-linux-amd64
./civitai-tester-linux-amd64

# Or on Windows
# Extract civitai-tester-windows-amd64.zip
civitai-tester-windows-amd64.exe

# With automatic test execution
./civitai-tester-linux-amd64 --run
```

**Then visit:** `http://localhost:9999` 🌐

**You'll see:**
```
🚀 Civitai API Tester started!
⚡ WebSocket server ready for real-time updates
🌐 Dashboard available at: http://localhost:9999
📊 Click "Start Tests" to begin comprehensive API testing
```

The application will:

1. Start the web server on port 9999
2. Wait for manual test execution (click "Start Tests" or use `--run` flag)
3. Display results in real-time at <http://localhost:9999>

### 🎛️ Command Line Options

```bash
./civitai-tester --help    # 📚 Show help information
./civitai-tester --run     # 🚀 Auto-run tests on startup
```

## ⚙️ Configuration

>[!TIP]
> **Zero Config Start:** The tester works out of the box! Configuration is optional for customizing test limits and API settings.

### 🌍 Environment Variables

```bash
export CIVITAI_API_KEY="your_api_key_here"    # 🔑 Optional: Your Civitai API key
export TESTER_PORT="9999"                     # 🌐 Optional: Web server port (default: 9999)
export TEST_TIMEOUT="30"                      # ⏱️ Optional: Test timeout in seconds
```

### 📄 Configuration File

Create a `config.json` file in the same directory as the executable:

```json
{
  "_comment": "🚨 WARNING: Development tool only - keep secure!",
  "api_key": "your_api_key_here",
  "server_port": 9999,
  "test_timeout_seconds": 30,
  "test_limits": {
    "models_limit": 5,
    "images_limit": 5,
    "creators_limit": 5,
    "tags_limit": 10
  },
  "custom_tests": {
    "skip_rate_limit_test": false,
    "only_tests": [],
    "skip_tests": ["Test Rate Limiting"]
  }
}
```

**Quick setup:** Copy `config.example.json` to `config.json` and customize! 🎯

## 🧪 Tests Performed

>[!NOTE]
> **Comprehensive Coverage:** Every test includes detailed timing, error reporting, and validation of response structure!

The tester runs these comprehensive API tests:

| Test | Endpoint | What It Checks | Performance Target |
|------|----------|----------------|-------------------|
| 🔍 **API Health Check** | `/api/v1/models` | Basic connectivity & response | < 10s |
| 📋 **Get Models** | `/api/v1/models` | Model listing with pagination | < 15s |
| 🎯 **Get Model Details** | `/api/v1/models/{id}` | Individual model data retrieval | < 15s |
| 🔄 **Get Model Versions** | `/api/v1/model-versions/{id}` | Version-specific information | < 20s |
| 🖼️ **Get Images** | `/api/v1/images` | Image browsing functionality | < 15s |
| 👥 **Get Creators** | `/api/v1/creators` | Creator discovery features | < 15s |
| 🏷️ **Get Tags** | `/api/v1/tags` | Tag system functionality | < 10s |
| 🔎 **Search Models** | `/api/v1/models?query=anime` | Advanced search capabilities | < 15s |
| 📄 **Test Pagination** | `/api/v1/models` (cursor-based) | Pagination implementation | < 20s |
| ⚡ **Test Rate Limiting** | Multiple rapid requests | Rate limit handling | < 30s |


## 🏗️ Project Structure

```txt
cmd/civitai-tester/
├── 🎯 main.go                    # Main application server with WebSocket
├── ⚙️ config.go                  # Configuration management  
├── 🌐 static/                    # Web assets (served at runtime)
│   ├── 📄 index.html             # Main web interface
│   ├── 🎨 css/style.css          # Custom dark theme styles
│   └── ⚡ js/app.js               # Real-time WebSocket application
├── 📋 config.example.json        # Example configuration
├── 🔨 build.sh                   # Cross-platform build script
├── 🪟 build.bat                  # Windows build script  
├── 🚀 run.sh                     # Quick run script
├── 🤖 .github/workflows/         # GitHub Actions for releases
│   └── 📦 release.yml            # Automated multi-platform builds
├── 📝 .gitignore                 # Git ignore rules
└── 📖 README.md                  # This awesome file!
```

### 🛠️ Technologies Used

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Backend** | Go + Standard Library | HTTP server, WebSocket, JSON API |
| **Frontend** | TailwindCSS | Utility-first CSS framework |
| **Animations** | AnimeJS | Smooth transitions and effects |
| **Real-time** | WebSocket | Live updates and smart rendering |
| **Build** | GitHub Actions | Automated cross-platform releases |

## 🔨 Building from Source

>[!TIP]
> **Developer Friendly:** Simple build process with cross-platform scripts and automated releases via GitHub Actions!

### 📋 Prerequisites

- Go 1.21 or later
- Internet connection for testing

### 🏗️ Build for Current Platform

```bash
cd cmd/civitai-tester
go build -o civitai-tester main.go config.go
./civitai-tester
```

### 🌍 Cross-platform Build

Use the provided build scripts:

```bash
# 🐧 Unix/Linux/macOS
./build.sh

# 🪟 Windows  
build.bat
```

This creates optimized binaries for all supported platforms in the `builds/` directory:

```txt
builds/
├── civitai-tester-linux-amd64
├── civitai-tester-linux-arm64  
├── civitai-tester-windows-amd64.exe
├── civitai-tester-windows-arm64.exe
├── civitai-tester-darwin-amd64
└── civitai-tester-darwin-arm64
```

### 🤖 Automated Releases

>[!NOTE]
> **GitHub Actions Magic:** Every git tag automatically builds and releases binaries for all platforms!

```bash
# Create and push a release tag
git tag v1.0.0
git push origin v1.0.0

# 🤖 GitHub Actions will automatically:
# ✅ Build for all 6 platforms
# ✅ Create optimized binaries  
# ✅ Package with documentation
# ✅ Create GitHub release
# ✅ Upload all assets
```

## 🔑 API Key Usage (Optional!)

>[!TIP]
> **Start Without Auth:** Most CivitAI endpoints work without an API key! Add one later for higher rate limits and authenticated features.

While an API key is not required for most endpoints, providing one allows:

- 📈 **Higher rate limits** - More requests per minute
- 🔓 **Access to authenticated endpoints** - Private models, favorites
- 🧪 **More comprehensive testing** - Full API coverage
- ⚡ **Better performance** - Fewer rate limit delays

**Get your free API key:** [CivitAI Account Settings](https://civitai.com/user/account) 🆓

## 🔒 Security & Production Warnings

>[!DANGER]
> **🚨 CRITICAL SECURITY NOTICE** 
> 
> **This application is a development and testing tool ONLY. It is NOT designed for production environments.**

### 🚫 **DO NOT:**

- Expose this server to the public internet
- Run this on production servers  
- Use this in untrusted network environments
- Deploy this to cloud instances accessible from the web
- Share the server URL publicly
- Run this with elevated privileges in production systems

### ✅ **SAFE USAGE:**

- Run locally on your development machine (localhost only)
- Use for API testing and development purposes
- Keep it behind firewalls and private networks
- Use for internal team testing (secure networks only)
- Monitor API functionality during development

### 🛡️ **Security Considerations:**

- The server binds to all interfaces (0.0.0.0) by default
- No authentication or authorization mechanisms
- No rate limiting on the web interface
- No input validation for malicious requests
- No HTTPS/TLS encryption
- No protection against common web attacks

### 📝 **Production Alternative:**

For production API monitoring, consider:

- Professional monitoring services (Datadog, New Relic, etc.)
- Internal monitoring systems with proper security
- Custom monitoring solutions with authentication
- Cloud provider monitoring tools

## 🔧 Troubleshooting

>[!NOTE]
> **Self-Diagnostic:** The tester includes built-in health checks and detailed error reporting to help you quickly identify and resolve issues!

### 🐛 Common Issues

| Issue | Solution | Notes |
|-------|----------|-------|
| **Port already in use** | Change port: `TESTER_PORT=8080 ./civitai-tester` | Default port is 9999 |
| **API rate limiting** | Wait or set `skip_rate_limit_test: true` | Handled gracefully |
| **Network issues** | Check internet connection and firewall | Requires internet access |
| **WebSocket not connecting** | Refresh browser, check console | Auto-reconnect enabled |

### 🔍 Verbose Output

The application provides detailed console output:

```bash
# Example console output
====================================================================
⚠️  SECURITY WARNING: DEVELOPMENT/TESTING TOOL ONLY
====================================================================
Civitai API Tester - Starting server...
Configuration:
  Server Port: 9999
  Test Timeout: 30 seconds  
  API Key: Not set
  Test Limits: Models=5, Images=5, Creators=5, Tags=10

🌐 Web dashboard available at: http://localhost:9999
⚡ WebSocket server ready for real-time updates
📊 Click "Start Tests" or use --run flag to begin testing
```

### 🧪 Debug Mode

```bash
# Run with verbose logging
CIVITAI_DEBUG=true ./civitai-tester

# Or check WebSocket in browser console
# Press F12 → Console → Look for WebSocket messages
```

## 📄 License & Legal

>[!IMPORTANT]
> **License Information:** This tester is part of the go-civitai-sdk project and follows the same license terms. Please review the license before using in any commercial context.

[go-civitai-sdk](../../)

## 🤝 Contributing

>[!TIP]
> **Want to Help?** I welcome contributions! Whether it's bug fixes, new features, or documentation improvements - every contribution makes this tool better for everyone!

### 🛠️ Development Setup

```bash
# Clone the repository
git clone https://github.com/regiellis/go-civitai-sdk.git
cd go-civitai-sdk/cmd/civitai-tester

# Verify everything works
go mod download
go test -v

# Run the tester
go run main.go config.go
```

### 💡 What We'd Love Help With

- 🐛 **Bug Reports:** Found an issue? Please report it with details!
- ✨ **New Features:** Enhanced UI, additional tests, better error handling
- 🧪 **More Tests:** Help us test edge cases and error conditions  
- 📖 **Documentation:** Improve examples, guides, and troubleshooting
- 🎨 **UI Improvements:** Better animations, mobile support, accessibility
- ⚡ **Performance:** Optimize WebSocket usage, reduce memory footprint

### 📋 Pull Request Guidelines

1. 🧪 **Test your changes** - Ensure all tests pass
2. 📖 **Update documentation** - Keep README and examples current
3. 🎨 **Follow Go conventions** - Use `go fmt` and `go vet`
4. 📝 **Describe your changes** - Clear PR descriptions help reviews

## 🔗 Links & Resources

- 🌐 **[CivitAI Platform](https://civitai.com/)** - The amazing AI art community
- 📚 **[CivitAI API Docs](https://developer.civitai.com/docs/api/public-rest)** - Official API documentation
- 🔑 **[Get API Token](https://civitai.com/user/account)** - Your account settings  
- 🐙 **[Parent SDK Repository](../../)** - The go-civitai-sdk project
- 💬 **[Discussions](../../discussions)** - Questions and community
- 🎯 **[Issues](../../issues)** - Bug reports and feature requests
- 📦 **[Releases](../../releases)** - Download pre-built binaries



**Start testing the CivitAI API like a boss! 🚀**

---

**🎨 Part of the [go-civitai-sdk](../../) project by [Regi Ellis](https://github.com/regiellis)** - Built with ❤️ for the AI art community

![Go Gopher](https://img.shields.io/badge/Made%20with-Go%20Gopher%20Power-00ADD8?logo=go&logoColor=white) ![Real-time](https://img.shields.io/badge/Powered%20by-WebSocket%20Magic-4CAF50?logo=socket.io&logoColor=white) ![API Testing](https://img.shields.io/badge/Built%20for-API%20Testing%20Excellence-FF6B35)