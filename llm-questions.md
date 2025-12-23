# Example Questions for Domino UAT Testing

Ask your AI assistant these questions to test your Domino platform:

## Using VS Code MCP Shortcuts (Recommended for Copilot in Domino Workspace)

If using GitHub Copilot in a Domino workspace, use these built-in commands:

**1. Quick Authentication Test**
```
/mcp.domino-qa-server.quick_auth_test
```
This will popup an input prompt where you enter your `user_name` and `project_name`.

**2. Full End-to-End UAT (14 tests in 5 phases)**
```
/mcp.domino-qa-server.end_to_end_uat_protocol
```
This will popup an input prompt where you enter your `user_name` and `project_name`.

---

## Using MCP Prompts (Recommended for other AI clients)

**1. Quick Authentication Verification**
```
Use the quick_auth_test prompt with my credentials from @domino_project_settings.md
```

**2. Full End-to-End UAT (14 tests in 5 phases)**
```
Execute the end_to_end_uat_protocol using settings from @domino_project_settings.md
```

**3. Alternative: Direct Request**
```
Run end to end UAT testing on Domino. Use username 'integration-test' and project 'uat_test_project'. Show progress after each test.
```

## Using Individual Tools

**1. Workspace IDEs**
```
Test all workspace IDEs (Jupyter, RStudio, VSCode) for user 'integration-test' and project 'workspace_test'.
```

**2. Admin Portal**
```
Run admin portal UAT testing. Use username 'integration-test' and project 'admin_test'.
```

**3. Hardware Tiers**
```
Test workspace hardware tiers (small-k8s, medium-k8s, large-k8s) for user 'integration-test' and project 'uat_test_project'.
```

**4. Performance Testing**
```
Run performance tests for concurrent jobs with user 'integration-test' and project 'perf_test'.
```

**5. Cleanup**
```
Clean up all test resources for user 'integration-test' and project 'uat_test_project'.
```

## What Gets Tested

### 14-Test UAT Suite (via `end_to_end_uat_protocol` prompt)
**Phase 1: Core Functionality**
- User authentication, project operations, job execution, workspace operations

**Phase 2: Data & Environment**
- Environment operations, dataset operations, enhanced dataset operations

**Phase 3: Advanced Features**
- File management, collaboration features, model operations

**Phase 4: Enhanced Testing**
- Enhanced model operations, enhanced advanced job operations

**Phase 5: Comprehensive Suites**
- Admin UAT suite, user UAT suite

### Additional Capabilities
- **32 MCP Tools**: Individual testing tools for granular control
- **5 Performance Tools**: Concurrent jobs, workspaces, API stress testing, data throughput
- **3 IDEs**: Jupyter, RStudio, VSCode
- **All Hardware Tiers**: small-k8s, medium-k8s, large-k8s

## Requirements

- Provide `user_name` and `project_name` (or reference `@domino_project_settings.md`)
- User must have **admin access** for full testing
- Use test projects only (never production)
- Always clean up after testing
