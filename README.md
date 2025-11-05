# GitHub Copilot MCP Server

<div align="center">

[![npm version](https://img.shields.io/npm/v/@leonardommello/copilot-mcp-server.svg)](https://www.npmjs.com/package/@leonardommello/copilot-mcp-server)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js](https://img.shields.io/badge/node-%3E%3D22.0.0-brightgreen)](https://nodejs.org)

</div>

A Model Context Protocol (MCP) server that integrates GitHub Copilot CLI with MCP clients.

<img src=".github/img/github.svg" alt="GitHub Copilot MCP Server" /></i>

## Features

- **9 Tools** - Interactive Copilot commands for coding assistance
- **2 Resources** - Session history and management
- **3 Prompts** - Workflow templates for common tasks
- **Full MCP Support** - Compatible with Claude Desktop, Claude Code, Cline, and more

## Quick Start

### For use: 

Add to your configuration file:

```json
{
  "mcpServers": {
    "copilot": {
      "command": "npx",
      "args": ["-y", "@leonardommello/copilot-mcp-server"]
    }
  }
}
```

### Prerequisites

You need GitHub Copilot CLI installed and authenticated:

```bash
npm install -g @github/copilot
copilot /login
```

---

## Tools

| Tool | Description | Parameters |
|------|-------------|------------|
| **ask-copilot** | Ask Copilot for coding help, debugging, architecture | `prompt`, `context`, `model`, `allowAllTools` |
| **copilot-explain** | Get detailed code explanations | `code`, `model` |
| **copilot-suggest** | Get CLI command suggestions | `task`, `model` |
| **copilot-debug** | Debug code errors | `code`, `error`, `context` |
| **copilot-refactor** | Get refactoring suggestions | `code`, `goal` |
| **copilot-test-generate** | Generate unit tests | `code`, `framework` |
| **copilot-review** | Get code review with feedback | `code`, `focusAreas` |
| **copilot-session-start** | Start new conversation session | - |
| **copilot-session-history** | Get session history | `sessionId` |

---

## Resources

| Resource | URI | Description |
|----------|-----|-------------|
| **session-history** | `copilot://session/{sessionId}/history` | Access conversation history for a session |
| **sessions-list** | `copilot://sessions` | List all active sessions |

---

## Prompts

| Prompt | Description | Arguments |
|--------|-------------|-----------|
| **code-review-template** | Structured code review template | `code`, `language` |
| **debug-template** | Debug assistance template | `code`, `error`, `context` |
| **refactor-template** | Code refactoring template | `code`, `goal` |

---

## 🔌 AI Client Integration

This MCP server works with **any MCP-compatible client**. Below are detailed setup instructions for popular AI coding assistants.

### 📘 Claude Desktop (Recommended)

Claude Desktop is the most tested and recommended client for this MCP server.

**Configuration Path:**
- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
- **Linux**: `~/.config/Claude/claude_desktop_config.json`

**Method 1: NPX (No Installation Required)**
```json
{
  "mcpServers": {
    "copilot": {
      "command": "npx",
      "args": ["-y", "@leonardommello/copilot-mcp-server"]
    }
  }
}
```

**Method 2: Global Installation**
```bash
npm install -g @leonardommello/copilot-mcp-server
```

Then add to config:
```json
{
  "mcpServers": {
    "copilot": {
      "command": "copilot-mcp-server"
    }
  }
}
```

**Method 3: Local Development**
```json
{
  "mcpServers": {
    "copilot": {
      "command": "node",
      "args": ["/absolute/path/to/copilot-mcp-tool/dist/esm/examples/server/copilotMcpServer.js"]
    }
  }
}
```

**After Setup:**
1. Restart Claude Desktop
2. Look for the 🔌 icon in the bottom-right corner
3. Click it to see "copilot" in the connected servers list

---

### 🖥️ Claude Code (CLI)

Claude Code provides the fastest setup experience via CLI.

**Quick Setup:**
```bash
# Using npx (no installation)
claude mcp add copilot -- npx -y @leonardommello/copilot-mcp-server

# Or with global installation
npm install -g @leonardommello/copilot-mcp-server
claude mcp add copilot copilot-mcp-server
```

**Import from Claude Desktop:**
```bash
# If you already configured Claude Desktop
claude mcp add-from-claude-desktop
```

**Verify Connection:**
```bash
claude mcp list
# Should show: copilot (connected)
```

**Usage in Chat:**
```bash
/mcp  # Check server status
```

---

### 🎯 Cursor

Cursor supports both one-click and manual installation.

**Method 1: Manual Configuration**

Edit `~/.cursor/mcp.json` (create if it doesn't exist):

```json
{
  "mcpServers": {
    "copilot": {
      "command": "npx",
      "args": ["-y", "@leonardommello/copilot-mcp-server"]
    }
  }
}
```

**Method 2: Settings UI**
1. Open Cursor Settings (Cmd/Ctrl + ,)
2. Search for "MCP"
3. Click "Add MCP Server"
4. Name: `copilot`
5. Command: `npx -y @leonardommello/copilot-mcp-server`

---

### 🔧 VS Code with Cline Extension

[Cline](https://github.com/cline/cline) is a popular MCP-compatible VS Code extension.

**Setup:**

1. Install Cline extension from VS Code marketplace
2. Open Cline settings (gear icon in Cline panel)
3. Navigate to "MCP Servers" section
4. Add new server:

```json
{
  "mcpServers": {
    "copilot": {
      "command": "npx",
      "args": ["-y", "@leonardommello/copilot-mcp-server"]
    }
  }
}
```

**Alternatively**, edit VS Code `settings.json`:
```json
{
  "cline.mcpServers": {
    "copilot": {
      "command": "npx",
      "args": ["-y", "@leonardommello/copilot-mcp-server"]
    }
  }
}
```

---

### ⚡ Zed Editor

Zed has native MCP support built-in.

**Configuration File:** `~/.config/zed/mcp.json`

```json
{
  "mcpServers": {
    "copilot": {
      "command": "npx",
      "args": ["-y", "@leonardommello/copilot-mcp-server"]
    }
  }
}
```

**Or use Zed's UI:**
1. Open Zed Settings (Cmd/Ctrl + ,)
2. Go to "Extensions" → "MCP"
3. Add server with command: `npx -y @leonardommello/copilot-mcp-server`

---

### 🔮 Windsurf

**Configuration Path:** `~/.windsurf/mcp.json`

```json
{
  "mcpServers": {
    "copilot": {
      "command": "npx",
      "args": ["-y", "@leonardommello/copilot-mcp-server"]
    }
  }
}
```

---

### 🌊 Gemini CLI

Gemini CLI supports both project-wide and global MCP server installation.

**Global Installation:**
```bash
gemini mcp add copilot -- npx -y @leonardommello/copilot-mcp-server
```

**Project-Specific:**
```bash
# In your project directory
gemini mcp add --project copilot -- npx -y @leonardommello/copilot-mcp-server
```

**Verify:**
```bash
gemini mcp list
```

---

### 🎨 JetBrains AI Assistant

For IntelliJ IDEA, PyCharm, WebStorm, etc.

**Setup:**
1. Open Settings (Cmd/Ctrl + ,)
2. Navigate to: `Tools → AI Assistant → Model Context Protocol (MCP)`
3. Click "+" to add new MCP server
4. Configure:
   - **Name**: `copilot`
   - **Command**: `npx`
   - **Arguments**: `-y @leonardommello/copilot-mcp-server`

---

### 🚀 Other MCP Clients

This server is compatible with **any MCP-compliant client**. Generic configuration:

```json
{
  "mcpServers": {
    "copilot": {
      "command": "npx",
      "args": ["-y", "@leonardommello/copilot-mcp-server"]
    }
  }
}
```

**Additional Compatible Clients:**
- **Amp** - Configuration in `~/.amp/mcp.json`
- **Augment Code** - MCP settings in IDE
- **Roo Code** - Via settings panel
- **Qwen Coder** - CLI: `qwen mcp add copilot`

---

## ✅ Compatibility Matrix

| Client | Status | Installation Method | Notes |
|--------|--------|-------------------|-------|
| [Claude Desktop](https://claude.ai/download) | ✅ **Tested** | JSON config | Most stable, recommended |
| [Claude Code](https://docs.claude.com/en/docs/claude-code) | ✅ **Tested** | CLI command | Fastest setup |
| [Cursor](https://cursor.sh/) | ✅ Compatible | JSON / UI | Multiple setup options |
| [Cline (VS Code)](https://github.com/cline/cline) | ✅ Compatible | Extension settings | VS Code integration |
| [Zed](https://zed.dev/) | ✅ Compatible | Native MCP support | Built-in UI |
| [Windsurf](https://windsurf.ai/) | ✅ Compatible | JSON config | Simple setup |
| [Gemini CLI](https://github.com/jamubc/gemini-mcp-tool) | ✅ Compatible | CLI command | Project & global |
| [JetBrains AI](https://www.jetbrains.com/ai/) | ✅ Compatible | Settings UI | All JetBrains IDEs |
| Other MCP clients | ✅ Compatible | Standard MCP protocol | Universal support |

## How It Works

This MCP server acts as a bridge between MCP clients and the GitHub Copilot CLI:

1. **MCP Client** (Claude Desktop) → Calls tool via MCP protocol
2. **MCP Server** (This package) → Translates to Copilot CLI command
3. **GitHub Copilot CLI** → Processes request and returns response
4. **MCP Server** → Returns formatted response to client

**Benefits:**
- Use Copilot's AI models directly in Claude conversations
- Maintain session history across interactions
- Access specialized Copilot features (explain, debug, review, etc.)
- No need to switch between tools

---

## 🎯 Real-World Use Cases

### 1. Code Explanation & Learning
**Scenario**: Understanding complex code patterns

```javascript
// Ask Copilot to explain
const result = arr.map(x => x * 2).filter(x => x > 10);
```

**Response**:
> This code performs two operations on an array in sequence:
> 1. `.map(x => x * 2)` - Creates a new array by multiplying each element by 2
> 2. `.filter(x => x > 10)` - Filters that result to only keep values greater than 10
>
> For example, if `arr = [3, 5, 8]`, the result would be `[16]`

---

### 2. Debugging Assistance
**Scenario**: Finding bugs in your code

```javascript
// Buggy code
function sum(arr) {
  return arr.reduce((a) => a+b, 0);
}
```

**Error**: `ReferenceError: b is not defined`

**Copilot's Fix**:
```javascript
function sum(arr) {
  return arr.reduce((a, b) => a+b, 0);
}
```
> The reduce callback needs both the accumulator and the current value.

---

### 3. Security Refactoring
**Scenario**: Fixing SQL injection vulnerabilities

```javascript
// Vulnerable code
function getUserData(id) {
  return db.query('SELECT * FROM users WHERE id = ' + id);
}
```

**Copilot's Secure Version**:
```javascript
async function getUserData(id) {
  if (!id) return null;

  // Use parameterized query to prevent SQL injection
  const query = 'SELECT * FROM users WHERE id = ?';
  const user = await db.query(query, [id]);

  return user || null;
}
```
> **Key improvements**: Parameterized queries, input validation, async/await

---

### 4. Test Generation
**Scenario**: Generate comprehensive tests

```javascript
function isPrime(n) {
  if (n <= 1) return false;
  for (let i = 2; i * i <= n; i++) {
    if (n % i === 0) return false;
  }
  return true;
}
```

**Generated Jest Tests**:
```javascript
describe('isPrime', () => {
  it('should return false for numbers <= 1', () => {
    expect(isPrime(-5)).toBe(false);
    expect(isPrime(0)).toBe(false);
    expect(isPrime(1)).toBe(false);
  });

  it('should return true for prime numbers', () => {
    expect(isPrime(2)).toBe(true);
    expect(isPrime(3)).toBe(true);
    expect(isPrime(97)).toBe(true);
  });

  it('should return false for composite numbers', () => {
    expect(isPrime(4)).toBe(false);
    expect(isPrime(100)).toBe(false);
  });
});
```

---

### 5. Code Modernization
**Scenario**: Update legacy JavaScript to modern ES6+

```javascript
// Legacy code
function processData(data) {
  var result = [];
  for (var i = 0; i < data.length; i++) {
    result.push(data[i] * 2);
  }
  return result;
}
```

**Modern Version**:
```javascript
function processData(data) {
  return data.map(item => item * 2);
}
```
> **Benefits**: Cleaner, modern arrow function, immutable array operation

---

### 6. CLI Command Suggestions
**Task**: "List all files recursively and count them"

**PowerShell**:
```powershell
(Get-ChildItem -Recurse -File).Count
```

**Bash**:
```bash
find . -type f | wc -l
```

---

### 7. Multi-Model Support
**Compare responses across AI models**:

```javascript
// Ask the same question to different models
// GPT-5: More detailed technical explanations
// Claude Sonnet 4.5: More concise, practical answers
// Claude Haiku 4.5: Faster responses for simple queries
```

**Example**:
```
Use ask-copilot with model="gpt-5" and prompt="Explain async/await"
Use ask-copilot with model="claude-sonnet-4.5" and prompt="Explain async/await"
```

---

## 📚 Detailed Tool Examples

### ask-copilot
**General-purpose coding assistant**

```
📝 Prompt: "Write a TypeScript function to debounce user input"

🤖 Response: Complete implementation with TypeScript types, error handling, and usage examples
```

### copilot-explain
**Code explanation and education**

```javascript
📝 Code to explain:
const memoize = fn => {
  const cache = new Map();
  return (...args) => {
    const key = JSON.stringify(args);
    return cache.has(key) ? cache.get(key) : cache.set(key, fn(...args)).get(key);
  };
};

🤖 Explanation: "This is a memoization function that caches results..."
```

### copilot-suggest
**Command-line suggestions**

```
📝 Task: "Find all TypeScript files modified in the last 7 days"

🤖 Windows: Get-ChildItem -Recurse -Filter *.ts | Where-Object {$_.LastWriteTime -gt (Get-Date).AddDays(-7)}
🤖 Linux: find . -name "*.ts" -mtime -7
```

### copilot-debug
**Bug identification and fixes**

```javascript
📝 Buggy async code:
async function fetchData() {
  const data = await fetch('/api/data');
  return data.json;
}

❌ Error: "data.json is not a function"

✅ Fix: return data.json() // Add parentheses
```

### copilot-refactor
**Code quality improvements**

```javascript
📝 Goal: "Improve performance"

// Before
const result = array.filter(x => x > 0).map(x => x * 2);

// After
const result = array.reduce((acc, x) => {
  if (x > 0) acc.push(x * 2);
  return acc;
}, []);

💡 Benefit: Single pass through array instead of two
```

### copilot-test-generate
**Automated test creation**

```javascript
📝 Framework: "jest"

🧪 Generates: Unit tests, edge cases, integration tests, mock data
📊 Coverage: Positive cases, negative cases, boundary conditions
```

### copilot-review
**Code review with focus areas**

```javascript
📝 Focus: ["security", "performance"]

🔍 Reviews:
- SQL injection vulnerabilities
- XSS vulnerabilities
- N+1 query problems
- Memory leaks
- Inefficient algorithms
```

### copilot-session-start / copilot-session-history
**Conversation tracking**

```
📝 Start session: Creates unique session ID
💾 Track history: All prompts and responses saved
🔍 View history: Retrieve past conversations
♻️ Resume context: Continue previous discussions
```

---

## 🎨 Quick Examples

**Generate Code:**
```
Use ask-copilot to write a Python function that validates email addresses
```

**Explain Code:**
```
Use copilot-explain to explain this regex: /^[a-z0-9]+@[a-z0-9]+\.[a-z]{2,}$/i
```

**Debug:**
```
Use copilot-debug with code="function sum(arr) { return arr.reduce((a) => a+b, 0); }" and error="ReferenceError: b is not defined"
```

**Generate Tests:**
```
Use copilot-test-generate with code="function isPrime(n) { return n > 1 && ![...Array(n).keys()].slice(2).some(i => n % i === 0); }" and framework="jest"
```

**Review Code:**
```
Use copilot-review with code="..." and focusAreas=["security", "performance"]
```

**Session Management:**
```
Use copilot-session-start to begin a new tracked conversation
Use copilot-session-history to view conversation history
```

---

## AI Models

Select from available models:
- `claude-sonnet-4.5` (default)
- `claude-sonnet-4`
- `claude-haiku-4.5`
- `gpt-5`

Example:
```
Use ask-copilot with model="gpt-5" and prompt="Explain async/await"
```

---

## Requirements

### System Requirements
- **Node.js**: >= 22.0.0
- **npm**: >= 10.0.0

### GitHub Copilot
- **GitHub Copilot subscription**: Required ([Get Copilot](https://github.com/features/copilot))
- **GitHub Copilot CLI**: Must be installed and authenticated
  ```bash
  npm install -g @github/copilot
  copilot /login
  ```

---

## Troubleshooting

### Common Issues

**❌ "copilot command not found"**
```bash
# Install GitHub Copilot CLI
npm install -g @github/copilot

# Verify installation
copilot --version
```

**❌ "Not authenticated"**
```bash
# Login to GitHub Copilot
copilot /login

# Follow the authentication flow in your browser
```

**❌ "Node.js version too old"**
```bash
# Check your Node.js version
node --version  # Must be >= 22.0.0

# Update Node.js
# Using nvm (recommended)
nvm install 22
nvm use 22

# Or download from nodejs.org
```

**❌ "MCP server not responding"**
```bash
# Test the server directly
npx -y @leonardommello/copilot-mcp-server

# Check Claude Desktop logs
# macOS: ~/Library/Logs/Claude/
# Windows: %APPDATA%\Claude\logs\
```

**❌ "Permission denied" on Windows**
```bash
# Run as administrator or use npx without global install
npx -y @leonardommello/copilot-mcp-server
```

---

## FAQ

**Q: Do I need a GitHub Copilot subscription?**
A: Yes, this MCP server requires an active GitHub Copilot subscription and the Copilot CLI installed.

**Q: Can I use this with Claude Desktop?**
A: Yes! This is the primary use case. Just add the configuration to `claude_desktop_config.json`.

**Q: Does this work with VS Code?**
A: Yes, through the Cline extension or any other MCP-compatible VS Code extension.

**Q: What's the difference between this and using Copilot directly?**
A: This allows you to use Copilot's capabilities within Claude conversations, combining both AI assistants.

**Q: Is my code sent to both GitHub and Anthropic?**
A: Code you share in conversations goes through Claude's MCP protocol to Copilot CLI, which processes it according to GitHub's privacy policy.

**Q: Can I use this offline?**
A: No, both GitHub Copilot and MCP clients require internet connection.

---

## Development

### Building from Source

```bash
# Clone the repository
git clone https://github.com/leonardommello/copilot-mcp-server.git
cd copilot-mcp-server

# Install dependencies
npm install

# Build the project
npm run build

# Run locally
npm start

# Run tests
npm test
```

### Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Project Structure

```
copilot-mcp-server/
├── src/
│   ├── examples/
│   │   └── server/
│   │       └── copilotMcpServer.ts  # Main MCP server implementation
│   └── ...                          # MCP SDK core files
├── dist/                            # Compiled output
├── scripts/                         # Build scripts
└── package.json
```

---

## What is MCP?

The [Model Context Protocol (MCP)](https://modelcontextprotocol.io) is an open protocol that enables AI applications to securely access data and tools from different sources. Think of it as a universal connector for AI assistants.

**Key concepts:**
- **Servers** (like this package): Provide tools, resources, and prompts
- **Clients** (like Claude Desktop): Use these capabilities in conversations
- **Tools**: Actions the AI can perform (like calling GitHub Copilot)
- **Resources**: Data the AI can access (like session history)
- **Prompts**: Templates for common workflows

Learn more at [modelcontextprotocol.io](https://modelcontextprotocol.io)

---

## Links

- 📦 **npm Package**: https://www.npmjs.com/package/@leonardommello/copilot-mcp-server
- 💻 **GitHub Repository**: https://github.com/leonardommello/copilot-mcp-server
- 🐛 **Report Issues**: https://github.com/leonardommello/copilot-mcp-server/issues
- 🤖 **GitHub Copilot**: https://github.com/features/copilot
- 🔗 **Model Context Protocol**: https://modelcontextprotocol.io

---

## License

MIT License - see [LICENSE](LICENSE) file for details

## Author

Created by **Leonardo M. Mello** ([@leonardommello](https://github.com/leonardommello))

---

<div align="center">

**Built with ❤️ using the [Model Context Protocol](https://modelcontextprotocol.io)**

If this project helped you, please consider giving it a ⭐ on [GitHub](https://github.com/leonardommello/copilot-mcp-server)!

</div>
