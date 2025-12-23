# Domino QA LLM Client

**AI-Powered Testing Client for Domino Data Science Platform**

This client enables you to use AI assistants (like Claude, GPT-4, etc.) to perform comprehensive testing, validation, and performance analysis of your Domino Data Science Platform through natural language conversations.

The client connects to an MCP server that exposes **32 specialized tools** and **2 standardized prompts** for intelligent platform assessment, automated UAT workflows, and data-driven performance analysis.

---

## 🚀 **Choose Your Deployment Method**

There are **two ways** to use this QA MCP client:

### **Option 1: Run from Your Laptop/Client (Local Setup)**
Connect to Domino from your local machine using Cursor, Claude Desktop, or VSCode.
- ✅ Best for: Local development and testing
- ✅ Requires: Manual MCP server installation on your machine
- ✅ Follow this guide below (Quick Start section)

### **Option 2: Run Inside Domino Workspace (Recommended)**
Run the MCP server directly inside a Domino VS Code workspace with GitHub Copilot.
- ✅ Best for: Team collaboration and centralized testing
- ✅ Requires: Pre-built Domino environment (`quay.io/domino/field:qa_mcp_server`)
- ✅ **Follow this guide:** [README-Domino-Workspace.md](./README-Domino-Workspace.md)

**💡 Tip:** If you're working in Domino workspaces with your team, use **Option 2** for zero local setup and automatic credential management.

---

## 📋 **Quick Start (Option 1: Local Setup)**

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

### **7. Understanding MCP Tools & Prompts**

The MCP server provides two types of capabilities:

#### **32 MCP Tools** (organized in 5 categories)

**Core Job Execution (4 tools):**
```
run_domino_job | check_domino_job_run_status | check_domino_job_run_results | open_web_browser
```

**UAT Testing Suite (12 tools):**
```
test_user_authentication | test_project_operations | test_job_execution
test_workspace_operations | test_environment_operations | test_dataset_operations
test_file_management_operations | test_collaboration_features | test_model_operations
enhanced_test_dataset_operations | enhanced_test_model_operations | enhanced_test_advanced_job_operations
```

**Performance Testing (5 tools):**
```
performance_test_workspaces | performance_test_jobs | stress_test_api
performance_test_concurrent_jobs | performance_test_data_upload_throughput
```

**Comprehensive Suites (6 tools):**
```
run_master_comprehensive_uat_suite (ULTIMATE SUITE)
run_comprehensive_advanced_uat_suite | run_admin_uat_suite | run_user_uat_suite
run_comprehensive_split_uat_suite | cleanup_test_resources
```

**Platform Management (5 tools):**
```
create_project_if_needed | test_dataset_creation_and_upload
test_environment_and_hardware_operations | test_advanced_job_operations | enhanced_test_file_management
```

#### **2 MCP Prompts** (standardized workflows)

**Prompt 1: `quick_auth_test`**
- Quick authentication verification
- Executes `test_user_authentication` tool
- Verifies platform access with provided credentials
- **Usage:** `"Use the quick_auth_test prompt with my credentials from @domino_project_settings.md"`

**Prompt 2: `end_to_end_uat_protocol`**
- Comprehensive 14-test UAT suite with strict continuous execution
- Executes all 14 tests sequentially without pausing
- Automatic cleanup after completion
- **Usage:** `"Execute the end_to_end_uat_protocol using settings from @domino_project_settings.md"`

**Mandatory Test Sequence (Execute in this exact order):**
1. **test_post_upgrade_env_rebuild** - Environment build validation
2. **test_file_management_operations** - File operations (upload, download, move, rename)
3. **test_file_version_reversion** - File version control and reversion
4. **test_project_copying** - Project copying functionality
5. **test_project_forking** - Project forking functionality
6. **test_advanced_job_operations** - Advanced job operations
7. **test_job_scheduling** - Job scheduling workflows
8. **test_comprehensive_ide_workspace_suite** - All workspace IDEs (Jupyter, RStudio, VSCode)
9. **test_workspace_file_sync** - Workspace file synchronization
10. **test_workspace_hardware_tiers** - Hardware tier validation (small-k8s, medium-k8s, large-k8s)
11. **enhanced_test_dataset_operations** - Enhanced dataset operations
12. **test_model_api_publish** - Model API publishing
13. **test_app_publish** - Application publishing
14. **run_admin_portal_uat_suite** - Admin portal comprehensive validation

**Cleanup Phase (Executes after Test 14):**
- `cleanup_all_project_workspaces` - Removes all test workspaces
- `cleanup_all_project_datasets` - Removes all test datasets

### **8. UAT Testing Rules & Workflow**

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

### UAT Testing (14 core tests via `end_to_end_uat_protocol` prompt)
- User authentication and permissions
- Project operations (create, copy, fork)
- Job execution (Python/R, hardware tiers, scheduling)
- Workspace operations (Jupyter, RStudio, VSCode, all hardware tiers)
- Environment operations and hardware configurations
- Dataset operations (creation, snapshots, enhanced workflows)
- File management (upload, download, move, rename, version control)
- Collaboration features (sharing, permissions)
- Model operations (training, deployment, publishing)
- Admin UAT suite (execution management, infrastructure, configuration)
- User UAT suite (comprehensive user-facing features)

### Performance Testing (5 dedicated tools)
- Workspace performance (concurrent workspace launches)
- Job performance (parallel job execution)
- API stress testing (high-volume API calls)
- Concurrent job capacity (20+ parallel jobs)
- Data upload throughput analysis

### Comprehensive Suites (6 tools for complete platform validation)
- Master comprehensive UAT suite (ultimate validation)
- Comprehensive advanced UAT suite
- Admin UAT suite (platform administration features)
- User UAT suite (user-facing workflows)
- Split UAT suite (distributed testing)

## Example Questions

### Using MCP Prompts (Recommended)

**Quick Authentication Test:**
```
"Use the quick_auth_test prompt with my credentials from @domino_project_settings.md"
```

**Full End-to-End UAT (14 sequential tests with automatic cleanup):**
```
"Execute the end_to_end_uat_protocol using settings from @domino_project_settings.md"
```

### Using Individual Tools

**UAT Testing:**
```
"Run comprehensive UAT on Domino using username 'integration-test' and project 'uat_test_project'."

"Test all workspace IDEs for user 'integration-test' and project 'workspace_test'."

"Run admin portal UAT testing for user 'integration-test' and project 'admin_test'."
```

**Performance Testing:**
```
"Test workspace hardware tiers (small-k8s, medium-k8s, large-k8s) for user 'integration-test'."

"Run performance tests for concurrent jobs with user 'integration-test' and project 'perf_test'."

"Test data upload throughput for user 'integration-test' and project 'throughput_test'."
```

**Resource Management:**
```
"Clean up all test resources for user 'integration-test' and project 'uat_test_project'."
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

## MCP Server Capabilities Summary

- **32 MCP Tools**: Comprehensive testing and performance analysis tools
- **2 MCP Prompts**: Standardized workflows (`quick_auth_test`, `end_to_end_uat_protocol`)
- **14-Test UAT Suite**: Sequential platform validation from environment builds to admin portal
- **Strict Execution**: Continuous test execution without pauses, automatic cleanup
- **5 Performance Tools**: Load testing, stress testing, capacity analysis
- **All IDEs Supported**: Jupyter, RStudio, VSCode
- **All Hardware Tiers**: small-k8s, medium-k8s, large-k8s
- **Complete Admin Validation**: Execution, infrastructure, configuration, monitoring, security

---

**Tech Stack:**
- MCP Server: Python 3.11+ | FastMCP | python-domino v1.4.8
- Domino Platform: v5.x/6.x compatible
- AI Clients: Cursor, Claude Desktop, VSCode with GitHub Copilot
