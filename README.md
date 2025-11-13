# Domino QA LLM Client

**AI-Powered Testing Client for Domino Data Science Platform**

This client enables you to use AI assistants (like Claude, GPT-4, etc.) to perform comprehensive testing, validation, and performance analysis of your Domino Data Science Platform through natural language conversations.

## 📋 **Quick Start**

### **1. Prerequisites**
- Python 3.11+
- Access to a Domino Data Science Platform instance
- Domino API key
- AI assistant with MCP support (Cursor, Claude Desktop, etc.)

### **2. Install QA MCP Server**

First, set up the QA MCP Server that provides the testing tools:

```bash
# Clone or navigate to the qa_mcp_server directory
# Replace /path/to/qa_mcp_server with your actual path
cd /path/to/qa_mcp_server

# Install dependencies
uv pip install -e .
```

### **3. Configure Environment**

Create a `.env` file in the qa_mcp_server directory:
```dotenv
DOMINO_API_KEY='your_api_key_here'
DOMINO_HOST='https://your-domino-instance.com'
```

### **4. Configure MCP in Your AI Client**

#### **For Cursor IDE:**
Create or update `.cursor/mcp.json` (replace `/path/to/qa_mcp_server` with your actual path):
```json
{
  "mcpServers": {
    "domino_qa_server": {
      "command": "uv",
      "args": ["--directory", "/path/to/qa_mcp_server", "run", "domino_qa_mcp_server.py"]
    }
  }
}
```

#### **For Claude Desktop:**
Add to your Claude Desktop config (replace `/path/to/qa_mcp_server` with your actual path):
```json
{
  "mcpServers": {
    "domino_qa_server": {
      "command": "uv",
      "args": ["--directory", "/path/to/qa_mcp_server", "run", "domino_qa_mcp_server.py"]
    }
  }
}
```

### **5. Verify Installation**

Test the setup by asking your AI assistant:
```
"Test user authentication for user 'your_username' and project 'test_project'"
```

## What You Can Test

### Core Features (14 tests)
- Environment builds
- File operations (upload, download, move, rename, version control)
- Project operations (copy, fork)
- Jobs (Python/R, hardware tiers, scheduling)
- Workspaces (Jupyter, RStudio, VSCode, all hardware tiers)
- Datasets (creation, snapshots)
- Publishing (Model APIs, Apps)

### Admin Portal (7 categories)
- Execution management
- Infrastructure management
- Configuration management
- Monitoring & notifications
- Security & auditing

## Example Questions

```
"Run comprehensive UAT on Domino using username 'integration-test' and project 'uat_test_project'."

"Test all workspace IDEs for user 'integration-test' and project 'workspace_test'."

"Test workspace hardware tiers (small-k8s, medium-k8s, large-k8s) for user 'integration-test'."

"Run admin portal UAT testing for user 'integration-test' and project 'admin_test'."

"Clean up all test workspaces and datasets for user 'integration-test' and project 'uat_test_project'."
```

## Requirements

- **User Access**: Must have admin permissions for full testing
- **Test Projects**: Always use test project names (e.g., "uat_test_project", "qa-test-project")
- **Never test in production projects**
- **Cleanup**: Always clean up test resources after testing

## Files Included

- `llm-questions.md` - Example questions to ask your AI
- `uat-rule.mdc` - Cursor rules for UAT testing workflow
- `domino-settings.md` - Configuration parameters (if provided)

## Test Coverage

- **23/23 Requirements**: 100% coverage
- **All 3 IDEs**: Jupyter, RStudio, VSCode
- **All Hardware Tiers**: small-k8s, medium-k8s, large-k8s
- **All Admin Features**: Complete admin portal validation

---

**Compatible with Domino 5.x/6.x. Requires Python 3.11+ with FastMCP, requests, and dominodatalab library.**
