# Frappe Logging Analysis

## Overview
This document provides a comprehensive analysis of Frappe's logging system, including logging methods, log storage locations, and configuration options.

## Frappe Logging Methods

### 1. Core Logging Functions

#### `frappe.logger()` - Main Logger Function
# Returns a Python logger with StreamHandler capabilities for basic logging
- **Location**: `frappe/__init__.py` (lines 2288-2299)
- **Purpose**: Returns a Python logger with StreamHandler capabilities
- **Parameters**:
  - `module`: Logger name and log file name (default: "frappe")
  - `with_more_info`: Adds SiteContextFilter for additional context
  - `allow_site`: Site-specific logging (default: True)
  - `filter`: Custom filter function
  - `max_size`: Max file size in bytes (default: 100,000)
  - `file_count`: Number of backup files (default: 20)

#### `frappe.utils.logger.get_logger()` - Advanced Logger
# Application logger with site and bench level capabilities, rotating files, and custom filters
- **Location**: `frappe/utils/logger.py` (lines 16-87)
- **Purpose**: Application logger with site and bench level capabilities
- **Features**:
  - Rotating file handlers
  - Site-specific logging
  - Stream-only mode support
  - Custom formatters and filters

#### `frappe.utils.log()` - Simple Logging
# Simple logging function for events with minimal configuration
- **Location**: `frappe/utils/__init__.py` (lines 350-351)
- **Purpose**: Simple logging function for events
- **Usage**: `frappe.utils.log(event, details)`

### 2. Error Logging Methods

#### `frappe.utils.error.log_error()` - Error Logging
# Logs errors to Error Log DocType with Sentry integration and trace IDs
- **Location**: `frappe/utils/error.py` (lines 36-76)
- **Purpose**: Logs errors to Error Log DocType
- **Features**:
  - Creates Error Log documents in database
  - Integrates with Sentry for telemetry
  - Supports trace IDs for monitoring
  - Handles deferred inserts for read-only mode

#### `frappe.utils.error.log_error_snapshot()` - Exception Snapshot
# Captures exception snapshots with automatic filtering of excluded exception types
- **Location**: `frappe/utils/error.py` (lines 79-89)
- **Purpose**: Captures exception snapshots
- **Features**:
  - Excludes certain exception types (AuthenticationError, CSRF, etc.)
  - Uses deferred insert for performance

### 3. Database-Based Logging

#### Error Log DocType
# Database DocType for storing error tracebacks, methods, and reference information
- **Location**: `frappe/core/doctype/error_log/error_log.py`
- **Fields**:
  - `error`: Code field containing traceback
  - `method`: Title/method name
  - `reference_doctype`: Related DocType
  - `reference_name`: Related document name
  - `seen`: Boolean flag
  - `trace_id`: Monitoring trace ID

#### Activity Log DocType
# Tracks user activities, operations, and status with IP address logging
- **Location**: `frappe/core/doctype/activity_log/activity_log.py`
- **Purpose**: Tracks user activities and operations
- **Fields**:
  - `operation`: Login, Logout, Impersonate
  - `status`: Success, Failed, Linked, Closed
  - `user`: User performing action
  - `ip_address`: User's IP address
  - `reference_doctype/name`: Related document

#### Access Log DocType
# Tracks document access patterns and user interactions with documents
- **Location**: `frappe/core/doctype/access_log/access_log.py`
- **Purpose**: Tracks document access patterns
- **Function**: `make_access_log()` for creating access logs

## Log Storage Locations

### 1. Bench-Level Logs
**Directory**: `/home/frappe/frappe-bench/logs/`

#### Available Log Files:
- `frappe.log` - Main Frappe application logs
- `web.log` - Web server logs
- `web.error.log` - Web server error logs
- `scheduler.log` - Background job scheduler logs
- `schedule.log` - Scheduled job logs
- `schedule.error.log` - Scheduled job error logs
- `worker.log` - Background worker logs
- `worker.error.log` - Background worker error logs
- `database.log` - Database operation logs
- `redis-cache.log` - Redis cache logs
- `redis-cache.error.log` - Redis cache error logs
- `redis-queue.log` - Redis queue logs
- `redis-queue.error.log` - Redis queue error logs
- `redis-socketio.log` - SocketIO logs
- `redis-socketio.error.log` - SocketIO error logs
- `node-socketio.log` - Node.js SocketIO logs
- `node-socketio.error.log` - Node.js SocketIO error logs
- `bench.log` - Bench-level operations
- `backup.log` - Backup operation logs
- `active_users.log` - Active user tracking

### 2. Site-Level Logs
**Directory**: `/home/frappe/frappe-bench/sites/{site_name}/logs/`

#### Available Log Files:
- `frappe.log` - Site-specific Frappe logs
- `database.log` - Site-specific database logs
- `scheduler.log` - Site-specific scheduler logs
- `active_users.log` - Site-specific user activity

### 3. Log File Structure
- **Format**: `%(asctime)s %(levelname)s {module} %(message)s`
- **Rotation**: RotatingFileHandler with 100KB max size, 20 backup files
- **Encoding**: UTF-8

## Log Configuration

### 1. Environment Variables
- `FRAPPE_STREAM_LOGGING`: Enable stream-only logging (no files)
- `CI`: Reduces log level to ERROR in test environments
- `USE_PROFILER`: Enables profiling middleware

### 2. Log Levels
- **Default**: `logging.WARNING` (dev server) or `logging.ERROR` (production)
- **Configurable**: Via `frappe.utils.logger.set_log_level()`
- **Supported Levels**: ERROR, WARNING, WARN, INFO, DEBUG

### 3. Log Types in Database
**Location**: `frappe/model/__init__.py` (lines 123-138)

#### Supported Log DocTypes:
- Version
- Error Log
- Scheduled Job Log
- Event Sync Log
- Event Update Log
- Access Log
- View Log
- Activity Log
- Energy Point Log
- Notification Log
- Email Queue
- DocShare
- Document Follow
- Console Log

### 4. Log Cleanup
- **Location**: `frappe/core/doctype/log_settings/log_settings.py`
- **Function**: `clear_log_table()` for efficient log cleanup
- **Retention**: Configurable days (default: 90 days)
- **Method**: Creates temporary table, copies recent data, replaces original

## Logging Features

### 1. Site Context Filter
- **Location**: `frappe/utils/logger.py` (lines 90-98)
- **Purpose**: Adds site and form dictionary information to logs
- **Security**: Sanitizes sensitive data (passwords, tokens, keys)

### 2. Log Rotation
- **Handler**: RotatingFileHandler
- **Max Size**: 100,000 bytes per file
- **Backup Count**: 20 files
- **Location**: Both bench and site levels

### 3. Monitoring Integration
- **Trace IDs**: Generated for request tracking
- **Sentry Integration**: Automatic exception capture
- **Telemetry**: Optional error reporting

### 4. Security Features
- **Sanitization**: Removes sensitive data from logs
- **Blocklist**: password, passwd, secret, token, key, pwd
- **Site Isolation**: Site-specific log directories

## Usage Examples

### Basic Logging
```python
# Get a logger for a module
logger = frappe.logger("my_module")
logger.info("This is an info message")
logger.error("This is an error message")

# Simple event logging
frappe.utils.log("user_action", "User clicked button")
```

### Simple Error Logging with `frappe.log_error()`

#### Basic Usage
```python
import frappe

# Basic error logging with module name
def log_error(data):
	frappe.log_error(data, "purchase_payment_control")

# Log error with traceback
try:
	risky_operation()
except Exception as e:
	frappe.log_error(frappe.get_traceback(), "my_module")

# Log error with custom message
frappe.log_error(
	message=f"Failed to process order {order_id}",
	title="Order Processing Error"
)

# Log error with context
frappe.log_error(
	message=f"Database connection failed for user {frappe.session.user}",
	title="Database Error",
	reference_doctype="User",
	reference_name=frappe.session.user
)
```

#### Error Log Storage and Retrieval
```python
# Error logs are stored in Error Log DocType
# Location: frappe/core/doctype/error_log/error_log.py

# Get recent error logs
error_logs = frappe.get_all(
	"Error Log",
	filters={"seen": 0},  # Unseen errors
	fields=["name", "error", "method", "creation"],
	order_by="creation desc",
	limit=10
)

# Mark error as seen
frappe.db.set_value("Error Log", error_log_name, "seen", 1)

# Get error log details
error_doc = frappe.get_doc("Error Log", error_log_name)
print(error_doc.error)  # The actual error message/traceback
print(error_doc.method)  # The method/function name
```

#### Error Log File Locations
```bash
# Bench-level error logs
/home/frappe/frappe-bench/logs/frappe.log
/home/frappe/frappe-bench/logs/web.error.log
/home/frappe/frappe-bench/logs/scheduler.error.log
/home/frappe/frappe-bench/logs/worker.error.log

# Site-level error logs
/home/frappe/frappe-bench/sites/{site_name}/logs/frappe.log

# Database error logs (Error Log DocType)
# Accessible via Frappe Desk > Error Log
```

### Error Logging
```python
# Log an error with context
frappe.utils.error.log_error(
    title="Database Connection Failed",
    message="Unable to connect to database",
    reference_doctype="System Settings",
    reference_name="Database Config"
)

# Log exception snapshot
try:
    # Some operation
    pass
except Exception as e:
    frappe.utils.error.log_error_snapshot(e)
```

### Activity Logging
```python
# Create activity log
frappe.get_doc({
    "doctype": "Activity Log",
    "operation": "Login",
    "user": "user@example.com",
    "status": "Success"
}).insert()
```

## Configuration Files

### 1. Site Configuration
- **File**: `sites/{site_name}/site_config.json`
- **Key Settings**: `developer_mode`, `maintenance_mode`

### 2. Common Site Configuration
- **File**: `sites/common_site_config.json`
- **Key Settings**: Redis URLs, ports, worker counts

## Best Practices

1. **Use Appropriate Log Levels**: ERROR for errors, WARNING for warnings, INFO for important events
2. **Include Context**: Use `with_more_info=True` for detailed context
3. **Site-Specific Logging**: Enable site-specific logs for multi-site deployments
4. **Regular Cleanup**: Configure log retention periods
5. **Security**: Be mindful of sensitive data in logs
6. **Performance**: Use deferred inserts for high-volume logging

## Troubleshooting

### Common Issues
1. **Empty Log Files**: Check log levels and permissions
2. **Large Log Files**: Configure rotation settings
3. **Missing Logs**: Verify site configuration and paths
4. **Permission Errors**: Check file system permissions

### Debug Commands
```bash
# Check log file permissions
ls -la /home/frappe/frappe-bench/logs/

# Monitor logs in real-time
tail -f /home/frappe/frappe-bench/logs/frappe.log

# Check site-specific logs
tail -f /home/frappe/frappe-bench/sites/medico.local/logs/frappe.log
```

## Conclusion

Frappe provides a comprehensive logging system with both file-based and database-based logging capabilities. The system supports multiple log levels, automatic rotation, site-specific logging, and integration with monitoring tools. Understanding these logging mechanisms is crucial for debugging, monitoring, and maintaining Frappe applications.
