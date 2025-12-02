# Domino QA LLM Client

**AI-Powered Testing Client for Domino Data Science Platform**

This client enables you to use AI assistants (like Claude, GPT-4, etc.) to perform comprehensive testing, validation, and performance analysis of your Domino Data Science Platform through natural language conversations.

## 📋 **Quick Start (Start-to-Finish)**

### **1. Get the Required Repositories**
1. **LLM Client (this project)** – clone the base workspace you will open in Cursor/Claude:
   ```bash
   git clone https://github.com/dominodatalab/domino-qa-llm-client.git
   cd domino-qa-llm-client
   ```
   Open this folder in Cursor (preferred) or Claude Desktop so the assistant can read the files (e.g., use “Open Folder” in Cursor).
2. **MCP Server** – clone the testing toolchain next to the client:
   ```bash
   git clone https://github.com/dominodatalab/qa_mcp_server.git
   ```
   You will run this repo locally so the client can talk to Domino via MCP.

### **2. Prerequisites**
- Python 3.11+
- Access to a Domino Data Science Platform instance with admin permissions
- Domino API key
- AI assistant that supports MCP (Cursor, Claude Desktop, VSCode with Claude extension, etc.)

### **3. Install the QA MCP Server**

From the `qa_mcp_server` directory you cloned in step 1:

```bash
cd /path/to/qa_mcp_server
uv venv
uv pip install -e .
```

### **4. Configure the MCP Server Environment**

Create a `.env` file inside `qa_mcp_server`:
```dotenv
DOMINO_API_KEY='your_api_key_here'
DOMINO_HOST='https://your-domino-instance.com'
```

### **5. Point Your AI Client to the MCP Server**

#### **Cursor IDE**
Inside `domino-qa-llm-client`, update `.cursor/mcp.json` (replace `/path/to/qa_mcp_server` with the actual path):
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

#### **Claude Desktop**
Add to your Claude Desktop config:
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

#### **VSCode (with Github Copilot)**
Inside `domino-qa-llm-client`, create `.vscode/mcp.json` (replace `/path/to/qa_mcp_server` with the actual path):
```json
{
  "inputs": [],
  "servers": {
    "domino_qa_server": {
      "type": "stdio",
      "command": "uv",
      "args": ["--directory", "/path/to/qa_mcp_server", "run", "domino_qa_mcp_server.py"]
    }
  }
}
```

### **6. Verify the Setup**

In Cursor, Claude Desktop, or VSCode (with the `domino-qa-llm-client` folder open), ask:
```
"Test user authentication for user 'integration-test' and project 'uat_test_project'"
```
If the assistant replies with Domino test results, everything is wired up correctly.

### **7. UAT Testing Rules & Workflow**

This client includes comprehensive UAT testing rules to guide your AI assistant:
- **`.github/instructions/uat-rules.instructions`** - VScode rules file
- **`.cursor/rules/uat-rule.mdc`** - Cursor-specific rules file 

The UAT rules file defines:
- **End-to-End UAT Protocol**: Complete 14-test sequence that runs automatically
- **Test Execution Rules**: Continuous execution without pausing between tests
- **Mandatory Test Sequence**: All 14 tests from environment builds to admin portal validation
- **Cleanup Procedures**: Automatic resource cleanup after test completion
- **Safety Guidelines**: Protection against running tests in production environments

**Your AI assistant will automatically follow these rules when you request UAT testing.**

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

- `llm-questions.md` - Example questions to ask your AI assistant
- `.github/instructions/uat-rules.instructions` - UAT testing workflow rules for AI assistants
- `.cursor/rules/uat-rule.mdc` - Cursor-specific rules file (legacy)
- `domino_project_settings.md` - Project configuration parameters

## Test Coverage

- **23/23 Requirements**: 100% coverage
- **All 3 IDEs**: Jupyter, RStudio, VSCode
- **All Hardware Tiers**: small-k8s, medium-k8s, large-k8s
- **All Admin Features**: Complete admin portal validation

---

**Compatible with Domino 5.x/6.x. Requires Python 3.11+ with FastMCP, requests, and dominodatalab library.**
