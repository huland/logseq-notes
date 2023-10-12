- Environment variables
	- SAP_HOST=
	- SAP_DB_USER=
	- SAP_FILE_PATH=
	- SAP_INCOMING_INVOICE_FILE_PATH=
	- SAP_SMB_PORT=
	- SAP_SMB_DOMAIN=
	- SAP_SMB_SHARE=
- samba
	- ```python
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
- tags:: #vertis