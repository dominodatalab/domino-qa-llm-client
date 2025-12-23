# Running QA MCP Server in Domino Workspaces

**AI-Powered Testing Directly Inside Domino Workspaces with GitHub Copilot**

This guide explains how to use the QA MCP Server within Domino Data Science Platform workspaces using a pre-configured compute environment. This method eliminates local setup and provides immediate access to all 32 MCP tools and 2 prompts directly in your Domino VS Code workspace.

---

## Overview

Instead of running the MCP server locally on your machine, you can deploy it **inside a Domino workspace** using a custom compute environment. This approach:

✅ Eliminates local installation requirements  
✅ Provides immediate access to testing tools within Domino  
✅ Auto-configures GitHub Copilot Chat with MCP server  
✅ Ensures consistent environment across your team  
✅ Runs testing from inside the Domino platform itself  
✅ Uses workspace credentials automatically (no manual API key configuration)  

---

## Architecture

### Custom Compute Environment

The deployment uses a pre-built Domino compute environment (`quay.io/domino/field:qa_mcp_server`) that includes:

- **VS Code (code-server)**: Full VS Code experience in browser
- **GitHub Copilot Extensions**: Pre-installed and configured
- **MCP Server**: Auto-deployed at `/opt/domino/qa_mcp_server/`
- **MCP Configuration**: Injected into VS Code settings automatically

### How It Works

```
┌─────────────────────────────────────────────────────┐
│ Domino Workspace (VS Code)                          │
│                                                     │
│  ┌──────────────────┐      ┌────────────────────┐   │
│  │ GitHub Copilot   │ ───> │ MCP Server         │   │
│  │ Chat             │      │ /opt/domino/       │   │
│  │                  │      │ qa_mcp_server/     │   │
│  └──────────────────┘      └────────────────────┘   │
│                                      │              │
│                                      ▼              │
│                             ┌────────────────────┐  │
│                             │ Domino API         │  │
│                             │ (uses workspace    │  │
│                             │  credentials)      │  │
│                             └────────────────────┘  │
└─────────────────────────────────────────────────────┘
```

When you launch a VS Code workspace in this environment:
- The MCP server is **immediately available** to GitHub Copilot Chat
- Workspace environment variables (`DOMINO_USER_API_KEY`, `DOMINO_API_HOST`) are **automatically used**
- No manual credential configuration required

---

## Prerequisites

1. **Domino Platform Access**
   - Domino Data Science Platform v5.x or v6.x
   - Admin permissions for comprehensive testing
   - Access to create/build Domino environments (or admin support)

2. **GitHub Account**
   - GitHub account with Copilot license
   - Ability to authenticate GitHub in VS Code

---

## Setup Instructions

### Step 1: Build the Domino Environment

**This is a Domino instance-level configuration (not project-level).**

1. Navigate to **Environments** in Domino (usually under Admin or Settings)
2. Click **"Create Environment"**
3. Configure the environment:
   - **Name:** "QA MCP Server Environment" (or your preferred name)
   - **Base Image:** `quay.io/domino/field:qa_mcp_server`
   - **Visibility:** Choose appropriate visibility (e.g., "Global" or "Organization")
4. Click **"Build"** or **"Create"**
5. Wait for the environment to build (usually 5-15 minutes)
6. Verify the environment shows as **"Ready"** or **"Active"**

**This pre-built environment includes:**
- VS Code (code-server)
- GitHub Copilot extensions
- MCP server at `/opt/domino/qa_mcp_server/`
- All necessary Python dependencies (Python 3.11+, FastMCP, python-domino v1.4.8)

**Note:** If you don't have permissions to create environments, contact your Domino administrator to build this environment for your team.

---

### Step 2: Create a Git-Based Domino Project

1. Log in to your Domino instance
2. Create a new project
3. Choose **"Create from Git"** option
4. Enter repository URL: `https://github.com/dominodatalab/domino-qa-llm-client.git`
5. Name your project (e.g., "domino-qa-testing" or "uat-test-project")
6. Click **"Create Project"**

This project contains all the instructions and example questions you'll need.

---

### Step 3: Configure Project to Use the Environment

1. In your Domino project, go to **Settings** → **Compute Environment**
2. Select the environment you built in Step 1: **"QA MCP Server Environment"**
3. Save the environment selection

---

### Step 4: Launch VS Code Workspace

1. In your Domino project, click **"Workspaces"**
2. Click **"New Workspace"**
3. Configure workspace:
   - **Name:** "QA-MCP-Workspace" (or your preferred name)
   - **Environment:** Should show the environment from Step 1
   - **Workspace IDE:** Select **"VS Code"**
   - **Hardware Tier:** Choose appropriate size (small/medium recommended for testing)
4. Click **"Launch"**
5. Wait for workspace to start (usually 1-2 minutes)

---

### Step 5: Connect GitHub Account in VS Code

Once the VS Code workspace opens in your browser:

1. Look at the **left sidebar** in VS Code
2. Click the **"Accounts"** icon (usually a person icon near the bottom)
3. Click **"Sign in with GitHub"**
4. Follow the authentication flow:
   - You'll be redirected to GitHub
   - Authorize the application
   - Return to VS Code workspace
5. Verify connection: You should see your GitHub username in the accounts section

**This step is required for GitHub Copilot to work.**

---

### Step 6: Start the MCP Server

1. In VS Code, click the **"Extensions"** icon in the left sidebar (four squares icon)
2. Look for **"mcp_qa_server"** in the list of installed extensions/tools
3. Click on **"mcp_qa_server"** to open its panel
4. Click the **"Start"** button (or similar activation control)
5. **Monitor the logs**: The MCP server will start outputting logs in the VS Code terminal/output panel
6. Wait for the server to show **"Ready"** or **"Server started"** message

**Expected log output:**
```
[MCP Server] Starting Domino QA MCP Server...
[MCP Server] Loading 32 tools...
[MCP Server] Loading 2 prompts...
[MCP Server] Server ready on stdio
```

---

### Step 7: Open GitHub Copilot Chat

1. In VS Code, look for the **chat icon** in the left sidebar (usually looks like a speech bubble)
2. Click to open **GitHub Copilot Chat**
3. The chat panel will open on the right side of VS Code

---

### Step 8: Start Interacting with the MCP Server

Now you can start testing! Open the `llm-questions.md` file in your project for example questions.

**Method 1: Using VS Code MCP Shortcuts (Recommended)**

In GitHub Copilot Chat, use these built-in commands:

**Quick authentication test:**
```
/mcp.domino-qa-server.quick_auth_test
```
This will popup an input prompt where you enter your `user_name` and `project_name`.

**Full UAT test (14 tests):**
```
/mcp.domino-qa-server.end_to_end_uat_protocol
```
This will popup an input prompt where you enter your `user_name` and `project_name`.

**Method 2: Using Natural Language Prompts**

**Quick verification test:**
```
Use the quick_auth_test prompt with my credentials from @domino_project_settings.md
```

**Full UAT test:**
```
Execute the end_to_end_uat_protocol using settings from @domino_project_settings.md
```

**Or browse `llm-questions.md` for more examples.**

---

## Step-by-Step Visual Guide

```
1. Build Environment → Domino Environments → quay.io/domino/field:qa_mcp_server
                ↓
2. Create Git Project → dominodatalab/domino-qa-llm-client.git
                ↓
3. Select Environment → Project Settings → QA MCP Server Environment
                ↓
4. Launch Workspace → VS Code IDE
                ↓
5. Connect GitHub → Left sidebar → Accounts → Sign in
                ↓
6. Start MCP Server → Extensions tab → mcp_qa_server → Start
                ↓
7. Open Copilot Chat → Chat icon in left sidebar
                ↓
8. Run Tests → Use examples from llm-questions.md
```

---

## Using the MCP Server in Domino Workspaces

### Method 1: Using MCP Prompts (Recommended)

MCP prompts are pre-configured workflows that guide GitHub Copilot through structured testing sequences.

**Quick Authentication Test:**
```
Use the quick_auth_test prompt with my credentials from @domino_project_settings.md
```

**Full End-to-End UAT (14 tests in 5 phases):**
```
Execute the end_to_end_uat_protocol using settings from @domino_project_settings.md
```

### Method 2: Direct Tool Invocation

You can also request specific tests directly:

**UAT Testing:**
```
Run comprehensive UAT on Domino using username 'integration-test' and project 'uat_test_project'
```

**Performance Testing:**
```
Run performance tests for concurrent jobs with user 'integration-test' and project 'perf_test'
```

**Resource Cleanup:**
```
Clean up all test resources for user 'integration-test' and project 'uat_test_project'
```

### Method 3: Browse Example Questions

Open `llm-questions.md` in your workspace to see:
- Quick authentication tests
- Full UAT workflows
- Performance testing examples
- Individual tool usage
- Cleanup procedures

---

## MCP Tools & Prompts Available

### 32 MCP Tools (5 Categories)

**Core Job Execution (4 tools):**
- `run_domino_job`, `check_domino_job_run_status`, `check_domino_job_run_results`, `open_web_browser`

**UAT Testing Suite (12 tools):**
- `test_user_authentication`, `test_project_operations`, `test_job_execution`
- `test_workspace_operations`, `test_environment_operations`, `test_dataset_operations`
- `test_file_management_operations`, `test_collaboration_features`, `test_model_operations`
- `enhanced_test_dataset_operations`, `enhanced_test_model_operations`, `enhanced_test_advanced_job_operations`

**Performance Testing (5 tools):**
- `performance_test_workspaces`, `performance_test_jobs`, `stress_test_api`
- `performance_test_concurrent_jobs`, `performance_test_data_upload_throughput`

**Comprehensive Suites (6 tools):**
- `run_master_comprehensive_uat_suite`, `run_comprehensive_advanced_uat_suite`
- `run_admin_uat_suite`, `run_user_uat_suite`, `run_comprehensive_split_uat_suite`
- `cleanup_test_resources`

**Platform Management (5 tools):**
- `create_project_if_needed`, `test_dataset_creation_and_upload`
- `test_environment_and_hardware_operations`, `test_advanced_job_operations`, `enhanced_test_file_management`

### 2 MCP Prompts (Standardized Workflows)

#### **Prompt 1: `quick_auth_test`**
- **Purpose:** Quick user authentication verification
- **What it does:** Executes `test_user_authentication` tool and verifies platform access
- **Returns:** Authentication status and basic platform connectivity check

#### **Prompt 2: `end_to_end_uat_protocol`**
- **Purpose:** Comprehensive 14-test UAT suite with strict continuous execution
- **Test Phases:**
  1. **Core Functionality** (4 tests): auth, projects, jobs, workspaces
  2. **Data & Environment** (3 tests): environments, datasets, enhanced datasets
  3. **Advanced Features** (3 tests): file mgmt, collaboration, models
  4. **Enhanced Testing** (2 tests): enhanced models, advanced jobs
  5. **Comprehensive Suites** (2 tests): admin suite, user suite
- **Execution Rules:**
  - Continuous execution (no pauses between tests)
  - No user confirmation requests
  - Cleanup only after all 14 tests complete
  - Single comprehensive report at end

---

## Understanding Prompts vs Tools

### Tools (`@mcp.tool()`)
- Execute code directly
- Return structured data (Dict[str, Any])
- Single-purpose operations
- Example: `test_user_authentication` runs one authentication test

### Prompts (`@mcp.prompt()`)
- Return formatted instruction strings
- Guide multi-step workflows
- Coordinate multiple tool calls
- Enforce execution patterns (like "no pauses")
- Example: `end_to_end_uat_protocol` orchestrates 14 tests in sequence

**When a prompt is invoked:**
1. Returns formatted markdown with configuration, task instructions, and tool calls
2. GitHub Copilot reads these instructions
3. Executes the appropriate tools in the specified order
4. Generates comprehensive reports

---

## Troubleshooting

### Issue: Can't Find the Environment

**Symptoms:**
- `quay.io/domino/field:qa_mcp_server` not available in project environment dropdown

**Solutions:**
1. Verify the environment was built at the instance level (Environments section, not project)
2. Check environment build status (should be "Ready" or "Active")
3. Verify environment visibility settings (should be accessible to your user/organization)
4. Contact Domino admin to build the environment if you don't have permissions

### Issue: MCP Server Not Responding

**Symptoms:**
- GitHub Copilot Chat doesn't execute MCP tools
- No test results returned

**Solutions:**
1. Check if MCP server is started (Extensions tab → mcp_qa_server → should show "Running")
2. Restart the MCP server from Extensions tab
3. Check MCP server logs in the Output/Terminal panel for errors
4. Verify the environment is using `quay.io/domino/field:qa_mcp_server` as base image
5. Restart the workspace if necessary

### Issue: GitHub Copilot Not Available

**Symptoms:**
- No Copilot Chat icon in left sidebar
- "Copilot not activated" errors

**Solutions:**
1. Verify you connected your GitHub account (Step 5)
2. Check your GitHub account has Copilot license
3. Sign out and sign back in to GitHub in VS Code
4. Check Extensions tab that Copilot extensions are installed and enabled

### Issue: MCP Server Won't Start

**Symptoms:**
- Errors when clicking "Start" on mcp_qa_server
- Logs show import errors or missing dependencies

**Solutions:**
1. Verify you're using the environment built from `quay.io/domino/field:qa_mcp_server`
2. Check workspace environment variables:
   ```bash
   echo $DOMINO_API_KEY
   echo $DOMINO_HOST
   ```
3. Check MCP server files exist:
   ```bash
   ls -la /opt/domino/qa_mcp_server/
   ```
4. Rebuild the environment if custom modifications were made

### Issue: Authentication Failures

**Symptoms:**
- Tools return authentication errors
- "Invalid API key" messages

**Solutions:**
1. Verify you have admin permissions on the Domino instance
2. Check workspace environment variables are available:
   ```bash
   echo $DOMINO_API_KEY
   echo $DOMINO_HOST
   ```
3. Contact your Domino admin if workspace credentials are not set

### Issue: Test Resources Not Cleaning Up

**Symptoms:**
- Old test projects/datasets remain after testing
- Naming collisions on subsequent tests

**Solutions:**
1. Manually run cleanup:
   ```
   Clean up all test resources for user 'integration-test' and project 'uat_test_project'
   ```
2. Check cleanup logs for errors
3. Verify user has delete permissions for projects/datasets

### Issue: "Prompt Not Found"

**Symptoms:**
- "Prompt not available" errors
- GitHub Copilot doesn't recognize prompt names

**Solutions:**
1. Verify MCP server version includes prompts
2. Check MCP server logs show "Loading 2 prompts..."
3. Restart MCP server from Extensions tab
4. Use direct tool invocation as alternative

---

## Safety Guidelines

⚠️ **CRITICAL SAFETY RULES:**

1. **Never run UAT in production projects**
   - Only use test project names (e.g., "uat_test_project", "qa-test-project")
   - Production projects could be damaged by test operations

2. **Always clean up test resources**
   - Run cleanup after every UAT session
   - Use `cleanup_test_resources()` tool

3. **Require admin permissions**
   - Full UAT requires admin access
   - Some tests will fail without proper permissions

4. **Use unique project names for each test run**
   - The MCP server generates unique names automatically
   - Don't override with hardcoded values

5. **Monitor resource usage**
   - Performance tests create concurrent workloads
   - Can impact platform resources if run excessively

---

## Benefits of Domino Workspace Deployment

### vs. Local Client Setup

| Aspect | Local Setup | Domino Workspace |
|--------|-------------|------------------|
| **Installation** | Manual clone & config | Pre-configured environment |
| **Credentials** | Manual API key setup | Automatic workspace credentials |
| **Consistency** | Varies by user machine | Identical across team |
| **Updates** | Manual git pull | Update environment once |
| **Network Access** | Requires external API access | Internal to Domino platform |
| **Collaboration** | Each user configures | Shared team environment |
| **Maintenance** | Per-user | Centralized |

### Advantages

✅ **Zero local setup** - Just launch workspace  
✅ **Pre-built environment** - Use `quay.io/domino/field:qa_mcp_server`  
✅ **Auto-credentials** - Uses workspace API key automatically  
✅ **Team consistency** - Everyone uses same environment  
✅ **Inside the platform** - Direct access to Domino internals  
✅ **GitHub Copilot integrated** - Ready to use after GitHub login  
✅ **Version control** - Git-based project with all instructions  

---

## Next Steps

1. **Build Environment:** Create environment from `quay.io/domino/field:qa_mcp_server` (Step 1)
2. **Create Project:** Git-based project from `dominodatalab/domino-qa-llm-client.git` (Step 2)
3. **Launch Workspace:** Start VS Code workspace with the custom environment (Steps 3-4)
4. **Connect GitHub:** Authenticate GitHub account for Copilot (Step 5)
5. **Start Server:** Activate MCP server from Extensions tab (Step 6)
6. **Verify Setup:** Run `quick_auth_test` prompt to confirm everything works (Step 8)
7. **Browse Examples:** Open `llm-questions.md` for example questions
8. **Run UAT:** Execute `end_to_end_uat_protocol` for comprehensive validation
9. **Team Onboarding:** Share environment and project with team members

---

## Quick Reference

**Environment Base Image:** `quay.io/domino/field:qa_mcp_server`

**Git Repository:** `https://github.com/dominodatalab/domino-qa-llm-client.git`

**MCP Server Location:** `/opt/domino/qa_mcp_server/`

**Example Questions:** See `llm-questions.md` in project

**Tech Stack:**
- Domino Platform: v5.x/6.x
- MCP Server: Python 3.11+ | FastMCP | python-domino v1.4.8
- VS Code: code-server (browser-based)
- AI: GitHub Copilot Chat with MCP protocol support
