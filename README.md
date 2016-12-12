Role Name: ssl-crt
=========

This role automates the process of creating a self-signed ssl certificate, usefull for local trusted networks. It creates a ssl key, csr, crt and optionally dhparam.pem file on the desired paths. This role can be included as a dependency with webserver roles like apache or nginx.

Requirements
------------

- openssl

Role Variables
--------------

Variables in 'defaults/main.yml' file are, which should be overridden:
- by role parameters, when this role is listed as a dependency by another role or at top playbook level
- other roles vars
- group/host vars

	ssl_dir: "/etc/pki/tls/certs"
	ssl_key_file: "/etc/pki/tls/private/{{ ansible_fqdn }}.key"
	ssl_key_size: "2048"
	ssl_csr_file: "/etc/pki/tls/certs/{{ ansible_fqdn }}.csr"
	ssl_csr_subject_fields: "\"/C=AL/ST={{ ssl_csr_state_province }}/L={{ ssl_csr_locality }}/O=Kot/CN={{ ansible_fqdn }}\""
	ssl_crt_file: "/etc/pki/tls/certs/{{ ansible_fqdn }}.crt"
	ssl_crt_days: "9999"
	ssl_dhparam_file: "/etc/pki/tls/private/dhparam.pem"
	ssl_dhparam_size: "4096"

The 'ssl_csr_state_province' and 'ssl_csr_locality' must be defined elsewhere by the user according to their location.

Dependencies
------------

None.

Example Playbook
----------------

	- hosts: servers
	    roles:
	      - ssl-crt
	        ssl_dir: "/path/to/dir"
	        ssl_crt_file: "/path/to/dir/server.crt"
	        ...

License
-------

BSD

Author Information
------------------

https://github.com/ichundu
