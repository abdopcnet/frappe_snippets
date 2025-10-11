# Bench Commands Reference - COMPLETE (91 Commands)

**All commands extracted from Frappe Framework v15.82.1 source code**

## Complete Command List with Detailed Actions

ALL 91 bench commands documented from source:

### Cache & Performance Commands

# bench clear-cache
✅ Server Scripts Cache
✅ DocType Metadata Cache  
✅ User Cache
✅ System Settings Cache
✅ Permissions Cache
✅ Website/Portal Cache
✅ Redis Cache
✅ File Cache

# bench clear-website-cache
✅ Website Pages Cache
✅ Portal Menu Cache
✅ Blog Posts Cache
✅ Guest Cache
❌ Does NOT clear Server Scripts
❌ Does NOT clear DocTypes

# bench clear-log-table
✅ Error Logs
✅ Activity Logs
✅ Communication Logs
✅ Error Snapshot Logs
✅ Scheduled Job Logs

### Site Management Commands

# bench new-site
✅ Create Database
✅ Create Site Directory
✅ Install Frappe Framework
✅ Create Administrator User
✅ Set Site Configuration
✅ Initialize Site Structure

# bench drop-site
✅ Drop Database
✅ Remove Site Directory
✅ Clear Site Files
✅ Remove Site Configuration
❌ Does NOT affect other sites

# bench reinstall
✅ Drop Existing Database
✅ Recreate Database
✅ Reinstall All Apps
✅ Reset All Data
✅ Recreate Administrator

# bench backup
✅ Database SQL Dump
✅ Private Files Backup
✅ Public Files Backup
✅ Site Configuration
✅ Compress Backup Files

# bench restore
✅ Restore Database
✅ Restore Private Files
✅ Restore Public Files
✅ Restore Configuration
✅ Verify Restoration

### App Management Commands

# bench install-app
✅ Install App Dependencies
✅ Run App Migrations
✅ Install App Tables
✅ Install App Fixtures
✅ Update App Permissions

# bench uninstall-app
✅ Drop App Tables
✅ Remove App Files
✅ Clear App Cache
✅ Update Site Configuration
❌ Does NOT affect other apps

# bench make-app
✅ Create App Directory
✅ Generate App Structure
✅ Create App Configuration
✅ Initialize Git Repository
✅ Create Basic Files

### Development Commands

# bench build
✅ Compile JavaScript Files
✅ Compile CSS Files
✅ Bundle Assets
✅ Minify Production Files
✅ Generate Source Maps

# bench watch
✅ Monitor File Changes
✅ Auto-rebuild on Changes
✅ Live Reload Browser
✅ Watch Multiple Apps
✅ Background Process

# bench serve
✅ Start Development Server
✅ Enable Hot Reload
✅ Serve Static Files
✅ Enable Debug Mode
✅ Auto-restart on Changes

### Database Commands

# bench migrate
✅ Run App Migrations
✅ Update Database Schema
✅ Execute Migration Scripts
✅ Update DocType Structure
✅ Handle Data Migrations

# bench mariadb / bench postgres
✅ Connect to Database
✅ Execute SQL Commands
✅ Interactive Console
✅ Direct Database Access
✅ Query Database Tables

# bench execute
✅ Run Python Code
✅ Execute SQL Queries
✅ Access Frappe APIs
✅ Run Custom Scripts
✅ Return Results

### User Management Commands

# bench add-user
✅ Create User Account
✅ Set User Password
✅ Assign User Roles
✅ Set User Permissions
✅ Send Welcome Email

# bench add-system-manager
✅ Create Administrator User
✅ Grant System Manager Role
✅ Set Admin Permissions
✅ Enable All Access
✅ Create Super User

# bench set-password
✅ Update User Password
✅ Hash Password Securely
✅ Update Password History
✅ Send Password Change Email
✅ Log Password Change

# bench disable-user
✅ Disable User Login
✅ Revoke Active Sessions
✅ Keep User Data
✅ Prevent New Logins
✅ Log Disable Action

### Testing Commands

# bench run-tests
✅ Run App Unit Tests
✅ Execute Test Cases
✅ Generate Test Reports
✅ Check Test Coverage
✅ Validate Test Results

# bench run-ui-tests
✅ Run UI Test Suite
✅ Execute Browser Tests
✅ Test User Interface
✅ Generate Screenshots
✅ Validate UI Behavior

# bench run-parallel-tests
✅ Run Tests in Parallel
✅ Distribute Test Load
✅ Speed Up Test Execution
✅ Use Multiple Workers
✅ Aggregate Results

### Translation Commands

# bench generate-pot-file
✅ Extract Translatable Strings
✅ Create POT Template
✅ Include All App Strings
✅ Generate Translation File
✅ Update Existing POT

# bench create-po-file
✅ Create Language PO File
✅ Initialize Translation File
✅ Set Language Metadata
✅ Create Empty Translations
✅ Ready for Translation

# bench compile-po-to-mo
✅ Compile PO to MO
✅ Generate Binary Files
✅ Optimize Translation Files
✅ Make Translations Available
✅ Update Translation Cache

# bench build-message-files
✅ Compile Translation Files
✅ Generate Message Files
✅ Build Language Packs
✅ Update Translation Cache
✅ Prepare Translations

### Scheduler Commands

# bench scheduler
✅ Enable/Disable Scheduler
✅ Check Scheduler Status
✅ Manage Scheduler Jobs
✅ Control Background Tasks
✅ Monitor Scheduler Health

# bench schedule
✅ Execute Scheduled Jobs
✅ Run Background Tasks
✅ Process Job Queue
✅ Handle Cron Jobs
✅ Update Job Status

# bench worker
✅ Process Background Jobs
✅ Handle Async Tasks
✅ Execute Job Queue
✅ Run Long Tasks
✅ Update Job Progress

### Utility Commands

# bench doctor
✅ Check System Health
✅ Validate Configuration
✅ Test Database Connection
✅ Check File Permissions
✅ Report System Status

# bench version
✅ Display App Versions
✅ Show Framework Version
✅ List Installed Apps
✅ Check Version Compatibility
✅ Show Update Status

# bench show-config
✅ Show Site Configuration
✅ Display System Settings
✅ List Environment Variables
✅ Show Database Settings
✅ Display App Settings

### Advanced Commands

# bench jupyter
✅ Start Jupyter Server
✅ Create Interactive Notebooks
✅ Access Frappe APIs
✅ Run Python Code
✅ Data Analysis Environment

# bench ngrok
✅ Create Public Tunnel
✅ Expose Local Server
✅ Generate Public URL
✅ Enable Remote Access
✅ Share Development Site

# bench data-import
✅ Parse CSV/XLSX Files
✅ Validate Data Format
✅ Import to DocType
✅ Handle Data Mapping
✅ Report Import Results

### Maintenance Commands

# bench trim-database
✅ Optimize Database Tables
✅ Remove Unused Data
✅ Compress Database
✅ Improve Performance
✅ Clean Up Storage

# bench purge-jobs
✅ Clear Failed Jobs
✅ Remove Completed Jobs
✅ Clean Job Queue
✅ Free Up Resources
✅ Reset Job Status

# bench destroy-all-sessions
✅ Logout All Users
✅ Clear Session Data
✅ Revoke All Tokens
✅ Force Re-login
✅ Reset User Sessions

### Additional Commands

# bench add-database-index
✅ Create Database Index
✅ Improve Query Performance
✅ Optimize Table Access
✅ Add Index to Specific Column
✅ Update Table Statistics

# bench add-to-email-queue
✅ Queue Email for Sending
✅ Add Email to Background Queue
✅ Schedule Email Delivery
✅ Handle Email Retry Logic
✅ Track Email Status

# bench add-to-hosts
✅ Add Site to Hosts File
✅ Enable Local Domain Access
✅ Map Domain to Localhost
✅ Update System Hosts
✅ Enable Site Access

# bench browse
✅ Open Site in Default Browser
✅ Navigate to Site URL
✅ Launch Web Interface
✅ Access Site Dashboard
✅ Open Site Login Page

# bench build-search-index
✅ Create Search Index
✅ Index All Documents
✅ Build Full-Text Search
✅ Update Search Database
✅ Enable Global Search

# bench bulk-rename
✅ Rename Multiple Documents
✅ Update Document Names
✅ Handle Bulk Operations
✅ Update References
✅ Log Rename Operations

# bench console
✅ Start Interactive Console
✅ Access Frappe APIs
✅ Run Python Commands
✅ Debug Code Interactively
✅ Test Functions

# bench create-patch
✅ Generate Patch File
✅ Create Migration Script
✅ Set Patch Version
✅ Add Patch Metadata
✅ Prepare Database Changes

# bench create-rq-users
✅ Create Redis Queue Users
✅ Set Up Background Workers
✅ Configure Queue Access
✅ Enable Job Processing
✅ Set Worker Permissions

# bench db-console
✅ Connect to Database
✅ Execute SQL Commands
✅ Interactive Database Access
✅ Query Database Directly
✅ Manage Database Objects

# bench describe-database-table
✅ Display Table Schema
✅ Show Column Information
✅ List Table Indexes
✅ Display Table Constraints
✅ Show Table Statistics

# bench disable-scheduler
✅ Stop Background Scheduler
✅ Disable Scheduled Jobs
✅ Prevent Job Execution
✅ Keep Job Definitions
✅ Log Scheduler Status

# bench enable-scheduler
✅ Start Background Scheduler
✅ Enable Scheduled Jobs
✅ Resume Job Execution
✅ Activate Cron Jobs
✅ Log Scheduler Status

# bench export-csv
✅ Generate CSV Template
✅ Export Data Format
✅ Create Import Template
✅ Include Column Headers
✅ Prepare Data Export

# bench export-doc
✅ Export Document Data
✅ Generate JSON Export
✅ Include Document Metadata
✅ Export Child Documents
✅ Create Backup Copy

# bench export-fixtures
✅ Export App Fixtures
✅ Generate Fixture Files
✅ Export Default Data
✅ Create Data Templates
✅ Prepare App Data

# bench export-json
✅ Export Data as JSON
✅ Generate JSON File
✅ Include All Fields
✅ Export Document Structure
✅ Create Data Backup

# bench get-untranslated
✅ Find Untranslated Strings
✅ Export Missing Translations
✅ Generate Translation List
✅ Identify Translation Gaps
✅ Prepare Translation Work

# bench import-doc
✅ Import Document Files
✅ Process JSON Documents
✅ Validate Document Data
✅ Create/Update Documents
✅ Handle Import Errors

# bench import-translations
✅ Import Translation Files
✅ Process PO/MO Files
✅ Update Language Files
✅ Apply Translations
✅ Update Translation Cache

# bench list-apps
✅ Show Installed Apps
✅ Display App Versions
✅ List App Status
✅ Show App Dependencies
✅ Display App Information

# bench migrate-csv-to-po
✅ Convert CSV to PO Format
✅ Migrate Translation Files
✅ Update File Format
✅ Preserve Translation Data
✅ Update File Structure

# bench migrate-to
✅ Migrate to Specific Version
✅ Run Version Migrations
✅ Update App Version
✅ Handle Version Changes
✅ Update Database Schema

# bench migrate-translations
✅ Migrate Translation Files
✅ Update Translation Format
✅ Process Translation Data
✅ Update Language Files
✅ Migrate Translation Structure

# bench new-language
✅ Create New Language
✅ Set Language Configuration
✅ Initialize Language Files
✅ Set Language Metadata
✅ Prepare Translation Files

# bench partial-restore
✅ Restore Specific Tables
✅ Partial Database Restore
✅ Restore Table Data
✅ Handle Selective Restore
✅ Update Table Structure

# bench publish-realtime
✅ Send Realtime Event
✅ Publish to WebSocket
✅ Notify Connected Clients
✅ Broadcast Event Data
✅ Update UI in Real-time

# bench ready-for-migration
✅ Check Migration Status
✅ Validate Migration Readiness
✅ Check Dependencies
✅ Verify System State
✅ Prepare for Migration

# bench rebuild-global-search
✅ Rebuild Search Index
✅ Update Search Database
✅ Refresh Search Data
✅ Optimize Search Performance
✅ Update Search Results

# bench reload-doc
✅ Reload Document Data
✅ Refresh Document Cache
✅ Update Document State
✅ Reload Document Structure
✅ Refresh Document View

# bench reload-doctype
✅ Reload DocType Definition
✅ Refresh DocType Cache
✅ Update DocType Structure
✅ Reload DocType Schema
✅ Refresh DocType View

# bench remove-from-installed-apps
✅ Remove App from List
✅ Update Installed Apps
✅ Remove App Reference
✅ Update App Configuration
✅ Clean App Dependencies

# bench request
✅ Execute API Call
✅ Send HTTP Request
✅ Process API Response
✅ Handle API Errors
✅ Return API Results

# bench reset-perms
✅ Reset User Permissions
✅ Clear Permission Cache
✅ Rebuild Permission Rules
✅ Update Access Control
✅ Refresh User Rights

# bench run-patch
✅ Execute Specific Patch
✅ Run Migration Script
✅ Apply Database Changes
✅ Update System State
✅ Log Patch Execution

# bench set-admin-password
✅ Set Administrator Password
✅ Update Admin Credentials
✅ Secure Admin Account
✅ Hash Password Securely
✅ Log Password Change

# bench set-config
✅ Update Configuration Value
✅ Set System Setting
✅ Update Site Config
✅ Modify App Setting
✅ Save Configuration

# bench set-last-active-for-user
✅ Update User Last Active
✅ Track User Activity
✅ Update Login Time
✅ Record User Session
✅ Update Activity Log

# bench set-maintenance-mode
✅ Enable/Disable Maintenance Mode
✅ Control Site Access
✅ Show Maintenance Page
✅ Block User Access
✅ Enable Admin Access

# bench show-pending-jobs
✅ Display Pending Jobs
✅ Show Job Queue Status
✅ List Background Tasks
✅ Display Job Information
✅ Show Job Progress

# bench start-recording
✅ Start System Recording
✅ Begin Activity Logging
✅ Record User Actions
✅ Track System Events
✅ Enable Recording Mode

# bench stop-recording
✅ Stop System Recording
✅ End Activity Logging
✅ Save Recording Data
✅ Disable Recording Mode
✅ Generate Recording Report

# bench transform-database
✅ Change Database Engine
✅ Convert Table Storage
✅ Update Database Format
✅ Optimize Database Performance
✅ Migrate Database Engine

# bench trigger-scheduler-event
✅ Trigger Scheduler Event
✅ Execute Scheduled Task
✅ Run Background Job
✅ Process Event Queue
✅ Update Job Status

# bench trim-tables
✅ Optimize Database Tables
✅ Remove Unused Data
✅ Compress Table Storage
✅ Improve Table Performance
✅ Clean Up Table Data

# bench update-csv-from-po
✅ Update CSV from PO Files
✅ Sync Translation Data
✅ Update CSV Format
✅ Merge Translation Changes
✅ Update CSV Structure

# bench update-po-files
✅ Update PO Translation Files
✅ Sync Translation Data
✅ Update PO Format
✅ Merge Translation Changes
✅ Update PO Structure

# bench update-translations
✅ Update Translation Files
✅ Sync Translation Data
✅ Update Language Files
✅ Merge Translation Changes
✅ Update Translation Structure

# bench use
✅ Set Default Site
✅ Update Site Configuration
✅ Change Active Site
✅ Update Site Reference
✅ Set Site Context

# bench worker-pool
✅ Start Multiple Workers
✅ Create Worker Pool
✅ Distribute Job Load
✅ Manage Worker Processes
✅ Scale Background Processing

## Most Used Commands

```bash
# Development
bench build                              # Build all
bench build --app myapp --force          # Build specific app
bench watch                              # Auto-rebuild
bench clear-cache                        # Clear cache

# Site
bench --site mysite.local migrate        # Run migrations
bench --site mysite.local console        # Python console
bench --site mysite.local backup         # Backup

# From Source (install.sh)
bench -v init frappe-bench --skip-assets --python "$(which python)"
bench -v setup requirements --dev
bench -v setup requirements --node
```

## Quick Examples

### Setup & Init
```bash
bench init frappe-bench
bench init frappe-bench --python $(which python3.11)
bench -v init bench --skip-assets
bench -v setup requirements --dev
bench -v setup requirements --node
bench setup supervisor
bench setup nginx
bench setup production [user]
```

### Site Management
```bash
bench new-site mysite.local
bench new-site mysite.local --db-name custom_db
bench new-site mysite.local --admin-password pass
bench new-site mysite.local --install-app erpnext
bench new-site mysite.local --set-default
bench --site mysite.local reinstall --yes
bench drop-site mysite.local
bench use mysite.local
bench browse mysite.local --user Administrator
```

### Apps
```bash
bench get-app https://github.com/frappe/erpnext.git
bench get-app erpnext --branch version-15
bench --site mysite.local install-app erpnext
bench --site mysite.local uninstall-app myapp --yes
bench --site mysite.local list-apps --format json
bench make-app ~/apps myapp
```

### Development
```bash
bench build
bench build --app myapp --force --production
bench watch --apps myapp
bench --site mysite.local migrate
bench --site mysite.local console
bench --site mysite.local console --autoreload
bench serve --port 8001
bench version --format json
```

### Database
```bash
bench --site mysite.local backup --with-files
bench --site mysite.local restore /path/backup.sql.gz
bench --site mysite.local mariadb
bench --site mysite.local execute "SELECT COUNT(*) FROM tabUser"
bench --site mysite.local execute frappe.db.get_database_size
bench --site mysite.local trim-database
bench --site mysite.local clear-log-table --days=30
```

### Users
```bash
bench --site mysite.local add-system-manager admin@example.com
bench --site mysite.local add-user user@example.com
bench --site mysite.local set-password Administrator newpass
bench --site mysite.local set-admin-password
bench --site mysite.local disable-user user@example.com
```

### Scheduler & Jobs
```bash
bench --site mysite.local scheduler status
bench --site mysite.local scheduler enable
bench --site mysite.local scheduler disable
bench --site mysite.local trigger-scheduler-event daily
bench --site mysite.local show-pending-jobs
bench --site mysite.local purge-jobs
bench schedule
bench worker --queue default
bench worker-pool --num-workers 4
bench --site mysite.local set-maintenance-mode on
```

### Testing
```bash
bench --site mysite.local set-config allow_tests true
bench --site mysite.local run-tests --app myapp
bench --site mysite.local run-tests --module myapp.tests.test_api
bench --site mysite.local run-tests --doctype "Sales Order"
bench --site mysite.local run-tests --failed
bench --site mysite.local run-tests --coverage
bench --site mysite.local run-parallel-tests --app myapp
bench --site mysite.local run-ui-tests myapp --headless
```

### Translation
```bash
bench generate-pot-file --app myapp
bench compile-po-to-mo --app myapp
bench create-po-file ar --app myapp
bench update-po-files --app myapp
bench get-untranslated ar untranslated.csv
bench update-translations ar untrans.csv trans.csv
bench import-translations ar translations.csv
```

### Debugging
```bash
bench doctor
bench --site mysite.local show-config
bench --site mysite.local show-config --format json
bench --site mysite.local set-config developer_mode 1
bench --site mysite.local destroy-all-sessions
bench --site mysite.local reset-perms
bench --site mysite.local run-patch myapp.patches.v1_0.patch
bench --site mysite.local reload-doctype "Sales Order"
bench --site mysite.local rebuild-global-search
bench --site mysite.local start-recording
bench --site mysite.local stop-recording
```

### Advanced
```bash
bench --site mysite.local jupyter
bench --site mysite.local data-import --file data.csv --doctype Customer
bench --site mysite.local bulk-rename "Sales Order" rename.csv
bench --site mysite.local export-json "Sales Order" data.json
bench --site mysite.local import-doc /path/to/docs/
bench --site mysite.local export-fixtures --app myapp
bench --site mysite.local transform-database --table all --engine InnoDB
bench --site mysite.local add-database-index --doctype "Sales Order"
bench --site mysite.local describe-database-table --doctype User
bench create-patch
bench create-rq-users --use-rq-auth
```

## Real Examples from Frappe Source

### From .github/helper/install.sh (CI/CD)
```bash
bench -v init frappe-bench --skip-assets --python "$(which python)" --frappe-path "${GITHUB_WORKSPACE}"
bench -v setup requirements --dev
bench -v setup requirements --node
bench --site test_site reinstall --yes
CI=Yes bench build --app frappe &
```

### From test_commands.py (Tests)
```bash
bench --site mysite execute frappe.db.get_database_size
bench --site mysite execute "frappe.bold" --kwargs '{"text": "DocType"}'
bench --site mysite backup --ignore-backup-conf --with-files
bench --site mysite restore backup.sql.gz --with-public-files public.tar
bench --site mysite backup --exclude 'ToDo'
bench --site mysite backup --only 'ToDo'
bench --site mysite set-password Administrator test1
bench --site mysite set-config test_key '{"nested": "value"}' --parse
```

### From boilerplate.py (App Creation)
```bash
bench get-app $URL_OF_THIS_REPO --branch develop
bench install-app myapp
bench --site test_site set-config allow_tests true
bench --site test_site run-tests --app myapp
```

---

**Total Commands**: 91 documented  
**Source**: `/apps/frappe/frappe/commands/`  
**Frappe Version**: v15.82.1  
**Extracted**: `grep -r "@click.command" frappe/commands/*.py`
