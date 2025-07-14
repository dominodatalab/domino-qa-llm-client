# Setup Guide for Domino QA LLM Client

## Quick Setup Steps

### 1. Environment Configuration

Create a `.env` file in the qa_mcp_server directory (replace with your actual path: `/path/to/qa_mcp_server/.env`):

```dotenv
# Required: Domino API Configuration
DOMINO_API_KEY=your_domino_api_key_here
DOMINO_HOST=https://your-domino-instance.com

# Optional: Default Test Configuration
DEFAULT_USER_NAME=your_username
DEFAULT_PROJECT_NAME=uat_test_project

# Optional: Performance Test Settings
DEFAULT_CONCURRENT_JOBS=20
DEFAULT_CONCURRENT_WORKSPACES=10
DEFAULT_TEST_DURATION=60
```

### 2. Install QA MCP Server

```bash
# Replace /path/to/qa_mcp_server with your actual path
cd /path/to/qa_mcp_server
uv pip install -e .
```

### 3. Configure Cursor MCP

The `.cursor/mcp.json` file is already configured in this directory. Restart Cursor to load the MCP server.

### 4. Test the Setup

Ask your AI assistant:
```
"Test user authentication for user 'your_username' and project 'test_project'"
```

## Getting Your Domino API Key

1. Log into your Domino Data Science Platform
2. Go to Account Settings (usually in the top-right menu)
3. Navigate to API section
4. Generate or copy your API key
5. Add it to the `.env` file

## Troubleshooting

### MCP Server Not Loading
- Check that the qa_mcp_server path in `.cursor/mcp.json` is correct
- Restart Cursor IDE
- Check Cursor's MCP logs for errors

### Authentication Errors
- Verify API key is correct
- Ensure DOMINO_HOST URL includes protocol (https://)
- Check user permissions in Domino platform

### Permission Errors
- Ensure your user has sufficient permissions in Domino
- Try with a simpler test first (authentication only)
- Check with Domino administrator if needed

## Next Steps

1. Run your first comprehensive test:
   ```
   "Run a master comprehensive UAT suite for user 'your_username' and project 'uat_test_project'"
   ```

2. Explore specific testing areas based on your needs
3. Set up regular monitoring workflows
4. Integrate with your CI/CD pipeline 