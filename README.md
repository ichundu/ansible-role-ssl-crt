Ansible role: ssl-crt
=====================

This role automates the process of creating a self-signed ssl certificate, either a RSA or ECC type certificate, defaults to RSA unless the `ssl_ecc_crt` variable is set to true. This is usefull for local trusted networks. It creates a ssl key, csr, crt and optionally dhparam.pem file on the desired paths. This role can be included as a dependency with webserver roles like apache or nginx.

Requirements
------------

- openssl

Role Variables
--------------

Variables in `defaults/main.yml` should be overridden with the desired values:

- by role parameters, when this role is listed as a dependency by another role or at top playbook level
- other roles vars
- group/host vars

Default variables:

|	Variable name	|	Default value	|	Description	|
|-------------------|-------------------|---------------|
| `ssl_ecc_crt`	| `false` | Weather to generate RSA or ECC certificate, defaults to RSA |
| `ssl_dir` | `/etc/pki/tls/certs` | Certificates directory |
| `ssl_key_file` | `/etc/pki/tls/private/{{ ansible_fqdn }}.key` | Certificate signing key file path |
| `ssl_rsa_key_size` | `2048` | RSA signing key size |
| `ssl_csr_file` | `/etc/pki/tls/certs/{{ ansible_fqdn }}.csr` | Certificate signing request file path |
| `ssl_csr_subject_fields` | `\"/C={{ ssl_csr_country }}/ST={{ ssl_csr_state_pro    vince }}/L={{ ssl_csr_locality }}/O={{ ssl_csr_ou }}/CN={{ ssl_csr_cn }}\"` | CSR subject fileds, other variables included here should be defined at the top playbook |
| `ssl_crt_file` | `/etc/pki/tls/certs/{{ ansible_fqdn }}.crt` | Self-signed certificate file path |
| `ssl_crt_days` | `9999` | Certificate valid days |
| `ssl_ecc_curve_name` | `secp384r1` | Default curve to use when generating the signing key |
| `ssl_dhparam_file` | `/etc/pki/tls/private/dhparam.pem` | DH group file path |
| `ssl_dhparam_size` | `4096` | DH group key size |

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

GPLv2

Author Information
------------------

https://github.com/ichundu
