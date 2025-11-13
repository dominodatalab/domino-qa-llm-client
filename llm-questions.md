# Example Questions for Domino UAT Testing

Ask your AI assistant these questions to test your Domino platform:

## Quick Tests

**1. Full Platform Test**
```
Run end to end UAT testing on Domino. Use username 'integration-test' and project 'uat_test_project'. Show progress after each test.
```

**2. Workspace IDEs**
```
Test all workspace IDEs (Jupyter, RStudio, VSCode) for user 'integration-test' and project 'workspace_test'.
```

**3. Admin Portal**
```
Run admin portal UAT testing. Use username 'integration-test' and project 'admin_test'.
```

**4. Hardware Tiers**
```
Test workspace hardware tiers (small-k8s, medium-k8s, large-k8s) for user 'integration-test' and project 'uat_test_project'.
```

**5. Cleanup**
```
Clean up all test workspaces and datasets for user 'integration-test' and project 'uat_test_project'.
```

## What Gets Tested

- **14 Core Tests**: Environment, projects, jobs, workspaces, datasets, publishing
- **Admin Portal**: All admin features (executions, infrastructure, configuration, monitoring, security)
- **3 IDEs**: Jupyter, RStudio, VSCode
- **Hardware Tiers**: small-k8s, medium-k8s, large-k8s

## Requirements

- Provide `user_name` and `project_name` in your question
- User must have **admin access** for full testing
- Use test projects only (never production)
- Always clean up after testing
