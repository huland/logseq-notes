- ## Possible configuration
	- ### Environment variables
		- SAP_HOST=
		- SAP_DB_USER=
		- SAP_FILE_PATH=
		- SAP_INCOMING_INVOICE_FILE_PATH=
		- SAP_SMB_PORT=
		- SAP_SMB_DOMAIN=
		- SAP_SMB_SHARE=
	- ### Secrets:
		- SAP_FILE_SERVER_USER=
		- SAP_FILE_SERVER_PASSWORD=
- ## Samba wrapper
	- `sap_smb.py`
	  collapsed:: true
		- ```python
		  def smb_connect():
		  	...
		      connection = SMBConnection(
		          read_secret('SAP_FILE_SERVER_USER'),
		          read_secret('SAP_FILE_SERVER_PASSWORD'),
		          my_name=os.environ.get('HOST_NAME'),
		          remote_name=os.environ.get("SAP_HOST",
		          domain=os.environ.get('SAP_SMB_DOMAIN'),
		          use_ntlm_v2=True,
		          is_direct_tcp=True,
		      )
		  	if connection.connect(
		        	os.environ.get("SAP_HOST", 
		  		port=int(os.environ.get('SAP_SMB_PORT'))
		  	):
		          return connection
		      else:
		          raise RuntimeError("SMB connection failed")
		      ...
		      
		      
		  def smb_retrieve_file(connection, file_path):
		    	...
		    	connection.retrieveFile(
		    		service_name=os.environ.get('SAP_SMB_SHARE'),
		      	path=file_path,
		      	file_obj=file_object
		    	)
		    	...
		  
		      
		  def smb_store_file(connection, file_path, file_object):
		      ...
		      filesize = connection.storeFile(
		          service_name=os.environ.get('SAP_SMB_SHARE'),
		          path=file_path,
		          file_obj=file_object,
		      )
		      ...
		  ```
- ## Background process
	- ### Collects data for `OUTGOING` invoices in MV2
		- updates the invoice's:
			- `invoice_number` to `transaction's slug`
			- `status` to `NORMAL_ISSUED`
		- update / create `InvoiceItem` with
			- update the:
				- `InvoiceItem's transaction` with the `invoice_number`
				- `InvoiceItem's ledger_account_code` with `B1T_Invoice.Account`
				- `InvoiceItem's cost_code` with `B1T_Invoice.CostCenter`
				- `InvoiceItem's cost_code2` with `B1T_Invoice.Project`
				- `InvoiceItem's net_amount_invoicing_in_system_currency` with `B1T_Invoice.Net_amount_in_LC`
				- `InvoiceItem's net_amount_invoicing_in_foreign_currency` with `B1T_Invoice.Net_amount_in_FC`
	- ### Collects data for `INCOMING` invoices in MV2
		- update / create `InvoiceItem` with
			- InvoiceItem's ledger_account_code with `B1T_PurchaseInvoice.Account`
			- InvoiceItem's cost_code with `B1T_PurchaseInvoice.CostCenter`
			- InvoiceItem's cost_code2 with `B1T_PurchaseInvoice.Project`
			- InvoiceItem's net_amount_invoicing_in_system_currency with `B1T_PurchaseInvoice.Net_amount_in_LC`
			- InvoiceItem's net_amount_invoicing_in_foreign_currency with `B1T_PurchaseInvoice.Net_amount_in_FC`
	- ### Sends email to the account owner with the:
		- transaction's slug
		- invoice attachment
- ## SAP and MV2 database mappings
	- B1T_Invoice.U_MVDocNum -> InvoiceData.id
	- B1T_Invoice.DocNum -> InvoiceData.invoice_number
	- B1T_Invoice.OrNumber -> Transaction.slug
	- B1T_Invoice.Account -> InvoiceItem.ledger_account_code
	- B1T_Invoice.CostCenter -> InvoiceItem.cost_code
	- B1T_Invoice.Project -> InvoiceItem.cost_code2
	- B1T_Invoice.Net_amount_in_LC -> InvoiceItem.net_amount_invoicing_in_system_currency
	- B1T_Invoice.Net_amount_in_FC -> InvoiceItem.net_amount_invoicing_in_foreign_currency
	- B1T_Invoice.ESignInvoice -> Contains the file path
		- ESignInvoice contains the filepath; the filepath is the last part
			- `filepath = ESignInvoice.split("\\")[-1]`
	- B1T_Invoice.U_MV2CardCode -> Account.account_code
	- ---
	- B1T_PurchaseInvoice.U_MVDocNum -> InvoiceData.id
	- B1T_PurchaseInvoice.OrNumber -> Transaction.slug
	- B1T_PurchaseInvoice.Account -> InvoiceItem.ledger_account_code
	- B1T_PurchaseInvoice.CostCenter -> InvoiceItem.cost_code
	- B1T_PurchaseInvoice.Project -> InvoiceItem.cost_code2
	- B1T_PurchaseInvoice.Net_amount_in_LC -> InvoiceItem.net_amount_invoicing_in_system_currency
	- B1T_PurchaseInvoice.Net_amount_in_FC -> InvoiceItem.net_amount_invoicing_in_foreign_currency
- tags:: #vertis