# Domino QA LLM Client

**AI-Powered Testing Client for Domino Data Science Platform**

This client enables you to use AI assistants (like Claude, GPT-4, etc.) to perform comprehensive testing, validation, and performance analysis of your Domino Data Science Platform through natural language conversations.

## 🎯 **What You Can Do**

Ask your AI assistant natural questions like:
- *"Is our Domino platform ready for production?"*
- *"Can the system handle 50 concurrent data science jobs?"*  
- *"Run a complete UAT test suite and generate a report"*
- *"Test user authentication and project operations"*
- *"What's our current performance baseline?"*

And get intelligent responses with automated test execution, performance metrics, and actionable recommendations.

## 🚀 **Available Capabilities**

### **32 MCP Tools from QA Server**

- **🔧 Core Job Execution (4 tools)**: Execute and monitor Domino jobs
- **🧪 UAT Testing Suite (12 tools)**: Comprehensive platform feature validation  
- **⚡ Performance Testing (5 tools)**: Load, stress, and capacity testing
- **🎯 Comprehensive Suites (6 tools)**: One-command complete assessments
- **🛠️ Platform Management (5 tools)**: Project, dataset, and resource management

### **Key Testing Areas**
- ✅ User authentication and permissions
- ✅ Project operations and collaboration
- ✅ Job execution and monitoring
- ✅ Workspace management
- ✅ Environment and hardware validation
- ✅ Dataset operations and file management
- ✅ Model deployment and management
- ✅ Performance and capacity testing

## 📋 **Setup Instructions**

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

## 💡 **Usage Examples**

### **Quick Health Check**
```
You: "Run a comprehensive UAT test for user 'john_doe' and project 'ml_project'"
AI: → Executes run_master_comprehensive_uat_suite()
Result: Complete platform assessment with pass/fail status for all features
```

### **Performance Testing**
```
You: "Test if our platform can handle 20 concurrent jobs"
AI: → Executes performance_test_concurrent_jobs()
Result: Performance metrics, capacity analysis, and recommendations
```

### **Specific Feature Testing**
```
You: "Test dataset operations for project 'data_science_proj'"
AI: → Executes enhanced_test_dataset_operations()
Result: Dataset creation, upload, access, and cleanup validation
```

### **Troubleshooting**
```
You: "Why are users having authentication issues?"
AI: → Executes test_user_authentication() + test_project_operations()
Result: Detailed authentication flow analysis with error diagnostics
```

## 🧪 **Testing Best Practices**

### **Recommended Test Sequence**
1. **Start with comprehensive suite**: `run_master_comprehensive_uat_suite`
2. **Use specific tests for issues**: Individual test functions for troubleshooting
3. **Always clean up**: Use `cleanup_test_resources` after testing
4. **Generate reports**: Document findings for stakeholders

### **Safety Guidelines**
- Always use test project names (e.g., "uat_test_project")
- Never run UAT tests in production projects
- Monitor resource usage during performance tests
- Clean up test resources after completion

### **Interpreting Results**
- **PASSED**: Feature working correctly
- **FAILED**: Issues detected - check error details
- **Performance metrics**: Compare against baselines
- **Pass rate < 100%**: Indicates system issues needing investigation

## 🔧 **Troubleshooting**

### **Common Issues**
- **Permission errors**: Check API key and user permissions
- **Connection errors**: Verify DOMINO_HOST URL format
- **Timeout errors**: Jobs/workspaces may need more time
- **Resource limits**: Check platform capacity during performance tests

### **Debug Steps**
1. Verify environment variables are set correctly
2. Test API connectivity with simple authentication test
3. Check Domino platform status and availability
4. Review detailed error messages in test results

## 📊 **Advanced Features**

### **Performance Baselines**
- Concurrent job capacity testing
- Data upload throughput analysis
- API stress testing capabilities
- Resource utilization monitoring

### **Automated Reporting**
- Structured JSON results for integration
- Pass/fail scoring with recommendations
- Performance metrics for analysis
- Natural language summaries

### **Smart Resource Management**
- Auto-generated unique test names
- Automatic cleanup procedures
- Graceful error handling and recovery
- Intelligent test sequencing

## 🚀 **Next Steps**

1. **Install and configure** the MCP server
2. **Run your first test** with comprehensive UAT suite
3. **Explore specific testing** for your use cases
4. **Set up monitoring** for ongoing platform health
5. **Integrate with CI/CD** for automated testing

## 📖 **Additional Resources**

- **QA MCP Server Repository**: `/path/to/qa_mcp_server`
- **Domino API Documentation**: Check your Domino instance docs
- **MCP Protocol**: [Model Context Protocol](https://github.com/modelcontextprotocol/typescript-sdk)

---

**Ready to transform your Domino platform testing?** Follow the setup instructions and start asking your AI assistant about your platform's health!

**Tech Stack**: MCP Protocol | Python 3.11+ | FastMCP | python-domino v1.4.8 | Domino v6.1+ 