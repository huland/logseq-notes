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
- samba
	- ```python filename sap_smb.py
	  def smb_connect():
	  	...
	      server_host = os.environ.get("SAP_HOST")
	      server_port = int(os.environ.get('SAP_SMB_PORT'))
	  
	      connection = SMBConnection(
	          read_secret('SAP_FILE_SERVER_USER'),
	          read_secret('SAP_FILE_SERVER_PASSWORD'),
	          my_name=os.environ.get('HOST_NAME'),
	          remote_name=server_host,
	          domain=os.environ.get('SAP_SMB_DOMAIN'),
	          use_ntlm_v2=True,
	          is_direct_tcp=True,
	      )
	  	if connection.connect(server_host, port=server_port):
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
- tags:: #vertis