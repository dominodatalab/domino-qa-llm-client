# Usage Examples for Domino QA LLM Client

## Common Testing Scenarios

### 1. Complete Platform Health Check

**Prompt:**
```
"Run a comprehensive UAT test suite for user 'john_doe' and project 'uat_test_project' including performance testing"
```

**What it does:**
- Executes `run_master_comprehensive_uat_suite`
- Tests all 32 tools across all platform features
- Includes performance and capacity testing
- Provides complete pass/fail assessment

---

### 2. Quick Authentication & Basic Functions Test

**Prompt:**
```
"Test user authentication and basic project operations for user 'alice_smith' and project 'test_project'"
```

**What it does:**
- Runs `test_user_authentication`
- Runs `test_project_operations`
- Verifies basic platform access and functionality

---

### 3. Performance Capacity Analysis

**Prompt:**
```
"Test if our platform can handle 25 concurrent jobs and measure data upload performance"
```

**What it does:**
- Executes `performance_test_concurrent_jobs` with concurrent_count=25
- Runs `performance_test_data_upload_throughput`
- Provides capacity metrics and recommendations

---

### 4. Troubleshooting Dataset Issues

**Prompt:**
```
"I'm having issues with dataset operations. Test dataset creation, upload, and management for project 'data_project'"
```

**What it does:**
- Runs `enhanced_test_dataset_operations`
- Tests dataset creation, upload, access, and cleanup
- Provides detailed diagnostics for dataset problems

---

### 5. Model Deployment Testing

**Prompt:**
```
"Test model operations and deployment workflows for project 'ml_models'"
```

**What it does:**
- Executes `enhanced_test_model_operations`
- Tests model creation, registration, and management
- Validates model deployment capabilities

---

### 6. Administrative Platform Assessment

**Prompt:**
```
"Run administrative tests to check infrastructure, monitoring, and system configuration"
```

**What it does:**
- Executes `run_admin_uat_suite`
- Tests infrastructure monitoring
- Validates system configuration
- Checks resource allocation

---

### 7. User Experience Validation

**Prompt:**
```
"Test the data scientist user experience including workspaces, collaboration, and workflows"
```

**What it does:**
- Runs `run_user_uat_suite`
- Tests authentication and access
- Validates workspace operations
- Checks collaboration features

---

### 8. API Stress Testing

**Prompt:**
```
"Stress test our API with 100 concurrent requests for 2 minutes"
```

**What it does:**
- Executes `stress_test_api` with concurrent_requests=100, test_duration=120
- Provides API performance metrics under load
- Identifies potential bottlenecks

---

### 9. Cleanup After Testing

**Prompt:**
```
"Clean up all test resources created during UAT testing for user 'test_user'"
```

**What it does:**
- Runs `cleanup_test_resources`
- Removes test projects, datasets, and other resources
- Provides cleanup status report

---

### 10. File Management Testing

**Prompt:**
```
"Test file upload, management, and operations for project 'file_test_project'"
```

**What it does:**
- Executes `enhanced_test_file_management`
- Tests file upload capabilities
- Validates file listing and management
- Tests multiple file types

---

## Advanced Usage Patterns

### Continuous Monitoring Setup

**Prompt:**
```
"Set up a baseline performance assessment for our platform that I can run regularly"
```

**Follow-up:**
```
"Run the same baseline test again and compare results with previous run"
```

### Capacity Planning

**Prompt:**
```
"Help me determine the maximum concurrent user capacity for our Domino platform"
```

**What happens:**
- Runs progressive performance tests
- Tests workspace capacity
- Tests job execution limits
- Provides scaling recommendations

### Pre-Production Validation

**Prompt:**
```
"We're about to go live with 50 data scientists. Validate our platform is ready for production load"
```

**What happens:**
- Comprehensive suite with high concurrency testing
- Full feature validation
- Performance baseline establishment
- Production readiness assessment

### Incident Investigation

**Prompt:**
```
"Users are reporting slow job execution. Help me diagnose the issue"
```

**What happens:**
- Targeted job execution testing
- Performance analysis
- Resource utilization check
- Diagnostic recommendations

## Tips for Effective Testing

1. **Always specify user and project names** for consistent testing
2. **Use test project names** (prefix with "uat_", "test_", or "qa_")
3. **Clean up after testing** to avoid resource accumulation
4. **Start with comprehensive suites** then drill down to specific issues
5. **Monitor platform load** during performance testing
6. **Document baselines** for comparison over time

## Natural Language Patterns

The AI assistant understands natural language, so you can ask:

- "Is our platform healthy?"
- "How many concurrent jobs can we handle?"
- "Why are workspaces taking so long to start?"
- "Test everything and give me a report"
- "Check if user permissions are working correctly"
- "What's our upload speed baseline?"
- "Clean up the mess from testing"

The more specific you are about what you want to test, the better the AI can help you! 