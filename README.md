Role Name: ssl-crt
=========

This role automates the process of creating a self-signed ssl certificate, usefull for local trusted networks. It creates a ssl key, csr, crt and optionally dhparam.pem file on the desired paths. This role can be included as a dependency with webserver roles like apache or nginx.

Requirements
------------

- openssl

Role Variables
--------------

Variables in 'defaults/main.yml' be overridden:

- by role parameters, when this role is listed as a dependency by another role or at top playbook level
- other roles vars
- group/host vars

Some variables are:

	ssl_dir: "/path/to/dir"
	ssl_key_file: "/path/to/srv.key"
	ssl_key_size: "2048"
	ssl_csr_file: "/path/to/srv.csr"
	ssl_csr_subject_fields: "\"/C={{ ssl_csr_country }}/ST={{ ssl_csr_state_province }}/L={{ ssl_csr_locality }}/O={{ ssl_csr_ou }}/CN={{ ssl_csr_cn }}\""
	ssl_crt_file: "/path/to/srv.crt
	ssl_crt_days: "9999"
	ssl_dhparam_file: "/path/to/dhparam.pem"
	ssl_dhparam_size: "4096"

The following variables must be defined elsewhere by the user according to their location:

- ssl_csr_country
- ssl_csr_state_province
- ssl_csr_locality
- ssl_csr_ou
- ssl_csr_cn

Dependencies
------------

None.

Example Playbook
----------------

	- hosts: servers
	    roles:
	      - ssl-crt
	        # additional role parameters/variables
	        ssl_dir: "/path/to/dir"
	        ssl_crt_file: "/path/to/dir/server.crt"
	        ...

License
-------

BSD

Author Information
------------------

https://github.com/ichundu
