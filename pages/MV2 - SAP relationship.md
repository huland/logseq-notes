- Environment variables
	- SAP_HOST=
	- SAP_DB_USER=
	- SAP_FILE_PATH=
	- SAP_INCOMING_INVOICE_FILE_PATH=
	- SAP_SMB_PORT=
	- SAP_SMB_DOMAIN=
	- SAP_SMB_SHARE=
- Secrets:
	- SAP_FILE_SERVER_USER=
	- SAP_FILE_SERVER_PASSWORD=
- Samba wrapper
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
- Background process
	- Collects the `OUTGOING` invoices from MV2
- SAP DB:
	- B1T_Invoice <--> MV2
		- U_MVDocNum <--> InvoiceData.id
		- DocNum <--> InvoiceData.invoice_number
		- OrNumber <--> Transaction.slug
		- Account <--> InvoiceItem.ledger_account_code
		- CostCenter <--> InvoiceItem.cost_code
		- Project <--> InvoiceItem.cost_code2
		- Net_amount_in_LC <--> InvoiceItem.net_amount_invoicing_in_system_currency
		- Net_amount_in_FC <--> InvoiceItem.net_amount_invoicing_in_foreign_currency
	- B1T_PurchaseInvoice <--> MV2
		- U_MVDocNum <--> InvoiceData.id
		- OrNumber <--> Transaction.slug
		- Account <--> ledger_account_code
		- CostCenter <--> cost_code
		- Project <--> cost_code2
		- Net_amount_in_LC <--> net_amount_invoicing_in_system_currency
		- Net_amount_in_FC <--> net_amount_invoicing_in_foreign_currency
- tags:: #vertis