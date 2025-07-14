# Domino QA Testing Configuration

This file contains all the configurable settings for your Domino QA testing. Modify these values to match your Domino environment and testing requirements.

## ⚠️ IMPORTANT: Admin User Requirements

**The user specified below MUST have ADMIN ACCESS to the Domino instance for comprehensive UAT and performance testing capabilities.**

Without admin access, many tests will fail due to insufficient permissions for:
- Creating/deleting test projects and workspaces
- Accessing system-level performance metrics
- Managing datasets and models across projects
- Running high-concurrency stress tests

## Test User Configuration

```bash
# Primary test user (requires admin permissions)
user_name="oussama"

# Test project for running tests (will be created if it doesn't exist)
project_name="uat_test_project"

# Optional: Secondary test user for collaboration testing
# collaborator_email="test.collaborator@yourcompany.com"
```

## Test Environment Settings

```bash
# Test project configuration
# The QA server will create and manage test projects with this prefix
test_project_prefix="uat-test"

# Default workspace settings for testing
test_workspace_template="Jupyter"
test_hardware_tier="small-k8s"

# Test timeout settings (in seconds)
test_timeout_seconds=300
job_timeout_seconds=600
workspace_startup_timeout=900

# Environment templates for testing (adjust to match your Domino instance)
test_environment_python="Python 3.11"
test_environment_r="R 4.3"
```

## Performance Test Configuration

### Workspace Performance Testing
```bash
# Number of workspaces to launch simultaneously
default_concurrent_workspaces=10

# Environment-specific recommendations:
# Small environment (1-10 users): 3-5
# Medium environment (10-50 users): 5-15  
# Large environment (50+ users): 10-30
```

### Job Performance Testing
```bash
# Number of jobs to run in parallel
default_concurrent_jobs=20

# Environment-specific recommendations:
# Small environment: 5-10
# Medium environment: 10-30
# Large environment: 20-50

# Job duration for performance testing (seconds)
default_job_duration=10
```

### API Stress Testing
```bash
# Requests per second for API stress testing
default_api_stress_requests=100

# Test duration for stress testing (seconds)
stress_test_duration=60

# Environment-specific recommendations:
# Small environment: 25-50 req/sec
# Medium environment: 50-200 req/sec
# Large environment: 100-500 req/sec
```

### Data Upload Performance
```bash
# File size for upload performance testing (MB)
default_upload_file_size_mb=10

# Number of files for concurrent upload testing
default_upload_file_count=5

# Test different file sizes: 1MB, 10MB, 100MB, 1GB
performance_test_file_sizes=[1, 10, 100, 1000]
```

## Environment-Specific Presets

Uncomment and use the preset that matches your Domino deployment:

### Small Environment (1-10 users)
```bash
# default_concurrent_workspaces=3
# default_concurrent_jobs=5
# default_api_stress_requests=25
# default_upload_file_size_mb=5
```

### Medium Environment (10-50 users)
```bash
# default_concurrent_workspaces=10
# default_concurrent_jobs=20
# default_api_stress_requests=100
# default_upload_file_size_mb=10
```

### Large Environment (50+ users)
```bash
# default_concurrent_workspaces=20
# default_concurrent_jobs=40
# default_api_stress_requests=200
# default_upload_file_size_mb=50
```

### Enterprise Environment (100+ users)
```bash
# default_concurrent_workspaces=30
# default_concurrent_jobs=60
# default_api_stress_requests=500
# default_upload_file_size_mb=100
```

## Test Data Configuration

```bash
# Sample data for testing (optional)
test_dataset_name="uat-sample-dataset"
test_model_name="uat-test-model"

# Test files for upload/download testing
test_file_types=["csv", "json", "parquet", "pkl", "txt"]
test_notebook_template="test_analysis.ipynb"

# Dataset testing
test_dataset_size_mb=50
test_dataset_records=10000
```

## Advanced Testing Configuration

### Hardware Tier Testing
```bash
# Test different hardware tiers (adjust based on your Domino configuration)
available_hardware_tiers=["small", "medium", "large"]
gpu_hardware_tiers=["gpu-small", "gpu-large"]
default_test_hardware="small"

# Advanced hardware testing
test_memory_intensive_workloads=true
test_gpu_workloads=false  # Set to true if GPU hardware available
```

### Environment and Language Testing
```bash
# Programming languages to test
test_languages=["python", "r"]
default_test_language="python"

# Custom environments for testing
custom_environments=[
    "Python Data Science",
    "R Statistical Computing", 
    "Spark Analytics"
]
```

### Collaboration Testing
```bash
# Multi-user testing configuration
enable_collaboration_tests=true
max_collaborators_per_project=5

# Project sharing and permissions testing
test_project_permissions=true
test_workspace_sharing=true
```

## Resource Cleanup Settings

```bash
# Automatic cleanup configuration
auto_cleanup_enabled=true
cleanup_delay_minutes=5

# Resources to clean up after testing
cleanup_test_projects=true
cleanup_test_workspaces=true
cleanup_test_datasets=true
cleanup_test_models=true
cleanup_test_jobs=false  # Keep job history for analysis

# Cleanup safety settings
max_cleanup_age_hours=24
cleanup_pattern_validation=true
```

## Reporting Configuration

```bash
# Report generation settings
default_report_format="markdown"  # Options: "markdown", "json", "html"
report_directory="./qa_reports"
report_timestamp_format="%Y%m%d_%H%M%S"

# Report content settings
include_detailed_logs=true
include_performance_graphs=false  # Requires additional visualization tools
include_screenshots=false
include_error_traces=true

# Report delivery
auto_generate_executive_summary=true
include_recommendations=true
include_capacity_analysis=true
```

## Performance Baseline Configuration

```bash
# Performance thresholds and expectations
expected_job_start_time_seconds=30
expected_workspace_start_time_seconds=120
expected_api_response_time_ms=1000

# Capacity planning targets
target_concurrent_users=50
target_job_throughput_per_hour=100
target_data_upload_speed_mbps=10

# Performance degradation alerts
performance_degradation_threshold_percent=20
capacity_utilization_warning_threshold=80
capacity_utilization_critical_threshold=95
```

## Integration Settings

### Monitoring Integration
```bash
# External monitoring integration (optional)
prometheus_enabled=false
grafana_dashboard_url=""
datadog_integration=false

# Alerting configuration
slack_webhook_url=""
email_notifications=false
teams_webhook_url=""
```

### CI/CD Integration
```bash
# Continuous integration settings
enable_automated_testing=false
ci_test_schedule="0 2 * * *"  # Daily at 2 AM
ci_performance_test_schedule="0 3 * * 0"  # Weekly on Sunday at 3 AM

# Quality gates
minimum_pass_rate_percent=95
maximum_performance_degradation_percent=10
```

### Custom Test Scripts
```bash
# Directory for custom test scripts
custom_scripts_directory="./custom_tests"

# Custom validation scripts
custom_python_validation="python custom_data_validation.py"
custom_r_validation="Rscript custom_model_validation.R"
custom_spark_test="spark-submit custom_spark_test.py"

# Custom performance benchmarks
custom_ml_benchmark="python ml_performance_benchmark.py"
custom_data_pipeline_test="python data_pipeline_stress_test.py"
```

## Security and Compliance Testing

```bash
# Security testing configuration
test_user_permissions=true
test_data_access_controls=true
test_api_authentication=true

# Compliance testing
test_data_privacy_controls=false  # Enable for regulated environments
test_audit_logging=true
test_backup_recovery=false  # Enable for production validation
```

## Advanced Configuration

### Retry and Resilience Settings
```bash
# Retry configuration for flaky tests
max_retries=3
retry_delay_seconds=10
exponential_backoff=true

# Circuit breaker settings
failure_threshold=5
recovery_timeout_seconds=300
```

### Resource Quotas and Limits
```bash
# Resource consumption limits during testing
max_cpu_cores_per_test=4
max_memory_gb_per_test=16
max_storage_gb_per_test=100

# Concurrent operation limits
max_concurrent_operations=50
rate_limit_requests_per_second=10
```

### Debugging and Diagnostics
```bash
# Debug configuration
enable_verbose_logging=false
capture_network_traces=false
save_test_artifacts=true

# Performance profiling
enable_performance_profiling=false
profile_memory_usage=false
profile_cpu_usage=false
```

## Usage Examples

To use these settings with the Domino QA MCP Server, reference them in your test commands:

```bash
# Using configured settings
"Run comprehensive UAT tests using my configured settings"

# Override specific settings  
"Launch 15 workspaces simultaneously instead of the default 10"

# Use environment-specific settings
"Run performance tests optimized for a large enterprise environment"

# Custom capacity testing
"Test our platform capacity with 25 concurrent jobs for 5 minutes"

# Specific feature testing
"Test dataset operations with 100MB files and validate upload performance"
```

## Configuration Validation Checklist

Before running tests, ensure:

### ✅ **Authentication & Access**
- [ ] User has admin access to the Domino instance
- [ ] API key is valid and configured in `.env` file  
- [ ] Domino host URL is correct in `.env` file
- [ ] Test user can create/delete projects and workspaces

### ✅ **Environment Validation**
- [ ] Hardware tiers exist in your Domino deployment
- [ ] Environment templates are available and functional
- [ ] Network connectivity allows API access
- [ ] Sufficient platform capacity for testing load

### ✅ **Resource Validation**
- [ ] Test project quotas are sufficient for testing
- [ ] Storage quotas allow for test file uploads
- [ ] Compute quotas support concurrent testing
- [ ] No existing resource conflicts

### ✅ **Configuration Accuracy**
- [ ] Performance thresholds match environment capacity
- [ ] Timeout values appropriate for environment speed
- [ ] Cleanup settings won't affect production resources
- [ ] Hardware tiers and environments exist as configured

## Troubleshooting Configuration Issues

### Common Configuration Problems

1. **User Permission Errors**
   ```
   Error: "Insufficient permissions to create project"
   Solution: Verify user has admin role in Domino platform
   ```

2. **Resource Limit Errors**
   ```
   Error: "Cannot launch workspace - quota exceeded"
   Solution: Reduce concurrent_workspaces or increase quotas
   ```

3. **Timeout Issues**
   ```
   Error: "Workspace startup timeout"
   Solution: Increase workspace_startup_timeout for slower environments
   ```

4. **Environment Issues**
   ```
   Error: "Environment template not found"
   Solution: Update test_environment_* settings to match available templates
   ```

5. **Network/API Issues**
   ```
   Error: "Connection timeout to Domino API"
   Solution: Check DOMINO_HOST URL and network connectivity
   ```

## Advanced Configuration Examples

### High-Performance Environment
```bash
# For high-capacity Domino instances
user_name="qa_admin"
project_name="performance_testing"
default_concurrent_workspaces=50
default_concurrent_jobs=100
default_api_stress_requests=1000
stress_test_duration=300
```

### Development Environment
```bash
# For smaller development instances
user_name="dev_admin"  
project_name="dev_qa_testing"
default_concurrent_workspaces=2
default_concurrent_jobs=5
default_api_stress_requests=20
stress_test_duration=30
```

### Regulated Environment
```bash
# For compliance-focused testing
test_data_privacy_controls=true
test_audit_logging=true
test_backup_recovery=true
enable_verbose_logging=true
save_test_artifacts=true
auto_cleanup_enabled=false  # Manual cleanup for audit trail
```

## Support and Documentation

For configuration assistance:

1. **Setup Issues**: Review the main `README.md` for installation instructions
2. **Test Scenarios**: Check `EXAMPLES.md` for common testing patterns  
3. **Performance Guidance**: Consult performance testing documentation
4. **Platform-Specific Help**: Contact your Domino administrator
5. **Advanced Configuration**: Refer to Domino API documentation

---

**🔧 Configuration Status**: Update this file with your specific Domino environment settings before running any tests. The QA agent will automatically reference these settings for all testing operations. 