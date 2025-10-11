# Frappe Client-Side Script Snippets (JavaScript)

**Based on:** Frappe v15.82.1 & ERPNext v15.79.1  
**Analyzed from:** Real production code in `/frappe/public/js` and `/erpnext/` doctypes

---

## Table of Contents
1. [Form Scripts](#form-scripts)
2. [Server Communication](#server-communication)
3. [Field Operations](#field-operations)
4. [UI Components](#ui-components)
5. [Database Operations](#database-operations)
6. [Utilities](#utilities)

---

## Form Scripts

### Basic Form Script Structure

```javascript
// Modern ES6 syntax (recommended in Frappe v15)
frappe.ui.form.on('DocType Name', {
	setup: function(frm) {
		// Called once when form is loaded
		// Set up queries, filters, and configurations
	},
	
	onload: function(frm) {
		// Called every time form loads
		// Initialize values, set defaults
	},
	
	refresh: function(frm) {
		// Called after form is loaded and rendered
		// Add custom buttons, show/hide fields
	},
	
	validate: function(frm) {
		// Called before save
		// Validate form data
		return true; // or false to prevent save
	},
	
	before_save: function(frm) {
		// Called just before document is saved
	},
	
	after_save: function(frm) {
		// Called after successful save
	},
	
	// Field change events
	field_name: function(frm) {
		// Called when field_name changes
	}
});
```

### Real Example: Sales Order (from ERPNext)

```javascript
frappe.ui.form.on('Sales Order', {
	setup: function(frm) {
		// Set query filters for link fields
		frm.set_query('bom_no', 'items', function(doc, cdt, cdn) {
			var row = locals[cdt][cdn];
			return {
				filters: {
					item: row.item_code
				}
			};
		});
		
		// Configure field properties
		frm.set_df_property('packed_items', 'cannot_add_rows', true);
		frm.set_df_property('packed_items', 'cannot_delete_rows', true);
	},
	
	refresh: function(frm) {
		if (frm.doc.docstatus === 1) {
			// Add custom button
			frm.add_custom_button(__('Create Invoice'), 
				() => frm.events.make_sales_invoice(frm),
				__('Create')
			);
		}
	},
	
	delivery_date: function(frm) {
		// Update all items delivery date
		$.each(frm.doc.items || [], function(i, d) {
			if (!d.delivery_date) d.delivery_date = frm.doc.delivery_date;
		});
		refresh_field('items');
	}
});
```

### Child Table Events

```javascript
frappe.ui.form.on('Sales Order Item', {
	item_code: function(frm, cdt, cdn) {
		var row = locals[cdt][cdn];
		
		if (frm.doc.delivery_date) {
			row.delivery_date = frm.doc.delivery_date;
			refresh_field('delivery_date', cdn, 'items');
		}
	},
	
	qty: function(frm, cdt, cdn) {
		var item = locals[cdt][cdn];
		// Recalculate on quantity change
		frm.script_manager.trigger('calculate_total', item.doctype, item.name);
	}
});
```

---

## Server Communication

### frappe.call() - Basic Usage

```javascript
// Basic call
frappe.call({
	method: 'frappe.client.get_value',
	args: {
		doctype: 'Customer',
		fieldname: 'customer_name',
		filters: { name: 'CUST-001' }
	},
	callback: function(r) {
		if (r.message) {
			console.log(r.message);
		}
	}
});
```

### frappe.call() - Advanced Options

```javascript
frappe.call({
	method: 'erpnext.selling.doctype.sales_order.sales_order.make_sales_invoice',
	args: {
		source_name: frm.doc.name,
		selected_items: items
	},
	freeze: true,
	freeze_message: __('Creating Invoice...'),
	callback: function(r) {
		if (!r.exc) {
			frappe.msgprint(__('Invoice created successfully'));
			frm.reload_doc();
		}
	},
	error: function(r) {
		frappe.msgprint(__('Failed to create invoice'));
	}
});
```

### frappe.xcall() - Promise-based (Modern)

```javascript
// Returns a promise
async function getData() {
	try {
		let result = await frappe.xcall('myapp.api.get_data', {
			param1: 'value1',
			param2: 'value2'
		});
		console.log(result);
	} catch (error) {
		frappe.msgprint(__('Error: ' + error));
	}
}
```

### Calling Document Methods

```javascript
// Call method defined in document controller
frm.call({
	method: 'calculate_taxes',
	doc: frm.doc,
	callback: function(r) {
		frm.refresh_fields();
	}
});

// Or with shorthand
frm.call('calculate_taxes');
```

---

## Field Operations

### Get and Set Values

```javascript
// Get value
let customer = frm.doc.customer;
let item_code = locals[cdt][cdn].item_code;

// Set value (triggers change event)
frm.set_value('customer', 'CUST-001');

// Set value without triggering (faster)
frm.doc.customer = 'CUST-001';
refresh_field('customer');

// Set multiple values
frm.set_value({
	customer: 'CUST-001',
	posting_date: frappe.datetime.get_today()
});
```

### Field Properties

```javascript
// Show/Hide field
frm.toggle_display('field_name', condition);

// Enable/Disable field
frm.toggle_enable('field_name', condition);

// Make field required
frm.toggle_reqd('field_name', true);

// Set field property
frm.set_df_property('field_name', 'read_only', 1);
frm.set_df_property('field_name', 'options', 'Customer');
frm.set_df_property('field_name', 'hidden', 1);

// Refresh single field
refresh_field('field_name');

// Refresh child table
frm.refresh_field('items');
```

### Query Filters (set_query)

```javascript
// Simple filter
frm.set_query('customer', function() {
	return {
		filters: {
			customer_type: 'Company',
			disabled: 0
		}
	};
});

// Filter child table field
frm.set_query('item_code', 'items', function(doc, cdt, cdn) {
	return {
		filters: {
			'is_sales_item': 1,
			'disabled': 0
		}
	};
});

// Custom query with server method
frm.set_query('contact_person', function() {
	return {
		query: 'frappe.contacts.doctype.contact.contact.contact_query',
		filters: {
			link_doctype: 'Customer',
			link_name: frm.doc.customer
		}
	};
});
```

---

## UI Components

### Custom Buttons

```javascript
// Add custom button
frm.add_custom_button(__('Create Invoice'), function() {
	// Button action
	create_invoice(frm);
});

// Add button to dropdown group
frm.add_custom_button(__('Payment Entry'), 
	() => make_payment(frm),
	__('Create')  // Group name
);

// Remove button
frm.remove_custom_button('Button Name');

// Set button as primary
frm.page.set_primary_action(__('Submit'), function() {
	frm.save('Submit');
});

// Set inner button group as primary
frm.page.set_inner_btn_group_as_primary(__('Create'));
```

### Messages and Alerts

```javascript
// Show message
frappe.msgprint(__('Record saved successfully'));

// Show message with title
frappe.msgprint({
	title: __('Success'),
	indicator: 'green',
	message: __('Record saved successfully')
});

// Show alert (temporary notification)
frappe.show_alert({
	message: __('Changes saved'),
	indicator: 'green'
}, 5);  // Duration in seconds

// Throw error (stops execution)
frappe.throw(__('Customer is required'));

// Confirm dialog
frappe.confirm(
	__('Are you sure you want to proceed?'),
	function() {
		// Yes action
		proceed_with_action();
	},
	function() {
		// No action (optional)
	}
);
```

### Dialogs

```javascript
// Simple dialog
let d = new frappe.ui.Dialog({
	title: __('Enter Details'),
	fields: [
		{
			label: 'Customer',
			fieldname: 'customer',
			fieldtype: 'Link',
			options: 'Customer',
			reqd: 1
		},
		{
			label: 'Date',
			fieldname: 'date',
			fieldtype: 'Date',
			default: frappe.datetime.get_today()
		}
	],
	primary_action_label: __('Submit'),
	primary_action: function(values) {
		console.log(values);
		d.hide();
	}
});
d.show();

// Dialog with table
let d = new frappe.ui.Dialog({
	title: __('Select Items'),
	fields: [
		{
			fieldname: 'items',
			fieldtype: 'Table',
			label: __('Items'),
			fields: [
				{
					fieldname: 'item_code',
					fieldtype: 'Link',
					label: __('Item'),
					options: 'Item',
					in_list_view: 1
				},
				{
					fieldname: 'qty',
					fieldtype: 'Float',
					label: __('Qty'),
					in_list_view: 1
				}
			]
		}
	],
	primary_action: function() {
		let values = d.get_values();
		let selected = d.fields_dict.items.grid.get_selected_children();
		console.log(selected);
		d.hide();
	}
});
d.show();
```

### Prompt

```javascript
// Simple prompt
frappe.prompt('Customer Name', function(values) {
	console.log(values);
});

// Multiple fields prompt
frappe.prompt([
	{
		label: 'Customer',
		fieldname: 'customer',
		fieldtype: 'Link',
		options: 'Customer',
		reqd: 1
	},
	{
		label: 'Amount',
		fieldname: 'amount',
		fieldtype: 'Currency'
	}
], function(values) {
	console.log(values.customer, values.amount);
}, __('Enter Details'));
```

---

## Database Operations

### frappe.db - Client-side Database API

```javascript
// Get single value
frappe.db.get_value('Customer', 'CUST-001', 'customer_name')
	.then(r => {
		console.log(r.message.customer_name);
	});

// Get multiple fields
frappe.db.get_value('Customer', 'CUST-001', ['customer_name', 'territory'])
	.then(r => {
		console.log(r.message);
	});

// Get value with filters
frappe.db.get_value('Customer', {customer_type: 'Company'}, 'name')
	.then(r => {
		console.log(r.message);
	});

// Check if document exists
frappe.db.exists('Customer', 'CUST-001')
	.then(exists => {
		if (exists) {
			console.log('Customer exists');
		}
	});

// Get list
frappe.db.get_list('Customer', {
	fields: ['name', 'customer_name'],
	filters: {
		customer_type: 'Company'
	},
	limit: 20,
	order_by: 'customer_name asc'
}).then(customers => {
	console.log(customers);
});

// Set value
frappe.db.set_value('Customer', 'CUST-001', 'customer_name', 'New Name')
	.then(r => {
		frappe.show_alert(__('Updated'));
	});

// Get single value from Settings
frappe.db.get_single_value('System Settings', 'country')
	.then(country => {
		console.log(country);
	});
```

---

## Utilities

### Date and Time

```javascript
// Get today's date
let today = frappe.datetime.get_today();

// Get now (datetime)
let now = frappe.datetime.now_datetime();

// Format date for display
let display_date = frappe.datetime.str_to_user(date_string);

// Parse user date to system format
let system_date = frappe.datetime.user_to_str(user_date);

// Add days
let future_date = frappe.datetime.add_days(date, 7);

// Add months
let next_month = frappe.datetime.add_months(date, 1);

// Get diff in days
let diff = frappe.datetime.get_day_diff(date1, date2);
```

### Number Formatting

```javascript
// Format number
let formatted = format_number(123456.789, '#,###.##');  // 123,456.79

// Format currency
let amount = format_currency(1000, 'USD');  // $1,000.00

// Parse float
let num = flt(value);  // Frappe float parser
let num = flt(value, 2);  // With precision

// Parse int
let int = cint(value);  // Frappe int parser
```

### String Operations

```javascript
// Translation
let text = __('Hello World');
let text = __('Hello {0}', [name]);

// Clean string
let cleaned = strip_html(html_string);

// Escape HTML
let safe = frappe.utils.escape_html(user_input);

// String formatting
let msg = frappe.utils.format('Hello {0}, you have {1} messages', ['John', 5]);
```

### Permissions

```javascript
// Check if user has permission
if (frappe.perm.has_perm('Customer', 0, 'write')) {
	// User can write
}

// Check model permission
if (frappe.model.can_create('Customer')) {
	// Can create
}

if (frappe.model.can_read('Customer')) {
	// Can read
}

// Check if user has specific role
if (frappe.user.has_role('Sales Manager')) {
	// User is Sales Manager
}

// Get current user
let user = frappe.session.user;
let full_name = frappe.session.user_fullname;
```

### Form Indicators

```javascript
// Set form indicator
frm.set_indicator_formatter('field_name', function(doc) {
	if (doc.status === 'Completed') {
		return 'green';
	} else if (doc.status === 'Pending') {
		return 'orange';
	} else {
		return 'red';
	}
});

// Page indicator
frm.page.set_indicator(__('Draft'), 'red');
```

### Freeze/Unfreeze UI

```javascript
// Freeze entire page
frappe.dom.freeze(__('Please wait...'));

// Unfreeze
frappe.dom.unfreeze();

// Auto freeze with call
frappe.call({
	method: 'myapp.api.long_operation',
	freeze: true,
	freeze_message: __('Processing...')
});
```

### Route/Navigation

```javascript
// Set route
frappe.set_route('List', 'Customer');
frappe.set_route('Form', 'Customer', 'CUST-001');
frappe.set_route('query-report', 'Sales Register');

// Get current route
let route = frappe.get_route();

// Reload page
location.reload();

// Go back
window.history.back();
```

### Local Storage

```javascript
// Set item
frappe.db.set_value('_session_cache', key, value);

// Get item
let value = frappe.boot.user_info[key];
```

---

## Advanced Patterns

### Custom Class Controllers

```javascript
// Extend form controller
frappe.ui.form.on('Sales Order', {
	setup: function(frm) {
		// Initialize custom controller
	}
});

// Create custom class
erpnext.selling.SalesOrderController = class SalesOrderController extends erpnext.selling.SellingController {
	onload(doc, dt, dn) {
		super.onload(doc, dt, dn);
	}
	
	refresh(doc, dt, dn) {
		super.refresh();
		
		// Custom logic
		if (this.frm.doc.docstatus == 1) {
			this.frm.add_custom_button(__('Make Invoice'), 
				() => this.make_sales_invoice()
			);
		}
	}
	
	make_sales_invoice() {
		frappe.model.open_mapped_doc({
			method: 'erpnext.selling.doctype.sales_order.sales_order.make_sales_invoice',
			frm: this.frm
		});
	}
};

// Use the controller
cur_frm.cscript = new erpnext.selling.SalesOrderController({frm: cur_frm});
```

### Realtime Updates (SocketIO)

```javascript
// Subscribe to realtime event
frappe.realtime.on('sales_order_update', function(data) {
	console.log('Received update:', data);
	frm.reload_doc();
});

// Publish event (from server-side Python)
// frappe.publish_realtime('sales_order_update', {'name': doc.name})
```

---

## Best Practices

1. **Use modern ES6 syntax** - Arrow functions, const/let
2. **Always use `__()`** for translation
3. **Use `frappe.xcall()`** for promise-based async calls
4. **Validate on client and server** - Never trust client validation alone
5. **Use `flt()` and `cint()`** for number conversions
6. **Refresh fields after changes** - `refresh_field('fieldname')`
7. **Handle errors gracefully** - Always add error callbacks

---

**Documentation generated from:** Frappe v15.82.1 | ERPNext v15.79.1  
**Last updated:** October 2025

