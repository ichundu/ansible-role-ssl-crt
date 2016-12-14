Ansible role: ssl-crt
=====================

This role automates the process of creating a self-signed ssl certificate, usefull for local trusted networks. It creates a ssl key, csr, crt and optionally dhparam.pem file on the desired paths. This role can be included as a dependency with webserver roles like apache or nginx.

Requirements
------------

- openssl

Role Variables
--------------

Variables in `defaults/main.yml` should be overridden with the desired values:

- by role parameters, when this role is listed as a dependency by another role or at top playbook level
- other roles vars
- group/host vars

Certificates directory:

	ssl_dir: "/path/to/dir"

`*.key` file path:

	ssl_key_file: "/path/to/srv.key"

Key size:

	ssl_key_size: "2048"

`*.csr`, certificate signing request file path:

	ssl_csr_file: "/path/to/srv.csr"

CSR subject fields:

	ssl_csr_subject_fields: "\"/C={{ ssl_csr_country }}/ST={{ ssl_csr_state_province }}/L={{ ssl_csr_locality }}/O={{ ssl_csr_ou }}/CN={{ ssl_csr_cn }}\""

`*.crt` file path:

	ssl_crt_file: "/path/to/srv.crt

Certificate valid days:

	ssl_crt_days: "9999"

DH parameters file path:

	ssl_dhparam_file: "/path/to/dhparam.pem"

DH parameters key size:

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

	  vars:
	    ssl_csr_country: "US"
	    ssl_csr_state_province: "Ohio"
	    ssl_csr_locality: "Rocky River"
	    ssl_csr_ou: "IT"
	    ssl_csr_cn: "Company"

	  roles:
	    - ichundu.ssl-crt

License
-------

BSD

Author Information
------------------

https://github.com/ichundu
