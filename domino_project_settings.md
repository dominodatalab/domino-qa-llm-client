# Domino QA MCP Server - Essential Parameters

## ⚠️ IMPORTANT: Admin User Requirements

**The user specified below MUST have ADMIN ACCESS to the Domino instance for comprehensive UAT and performance testing capabilities.**

## Core Required Parameters

### User & Project Settings
```
# Primary user for all testing (must have admin access)
USER_NAME=integration-test

# Default project for testing (will be created if doesn't exist)
PROJECT_NAME=uat_test_project
