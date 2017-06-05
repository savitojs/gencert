# Gencert

Utility to generate easy csr and self sign certificates.
  - Generate Key of 4096 key length with SHA512 Signature Algorithm
  - Generate certificate signing request (CSR) using anwerfile (config)
  - Generate Self sign certificates with SubjectAltName (SAN) support, Generates .csr, .key, .crt

## Usage
`gencert [-h] [-s, --selfsign] <fqdn> <csr_config>`
```
 -h                     Show this help
 -s, --selfsign         Generate self-signed certificate in addition to key and CSR.
 <fqdn>                 Output files will be named as <fqdn>.key and <fqdn>.csr.
 <csr_config>           Path to file that specifies CSR information.
```
## Prequesites
- Openssl binary
- Git

## Install

### Install Openssl and Git
For fedora systems

```
sudo dnf install openssl git
```

For RHEL/CentOS based systems

```
sudo yum install openssl git
```

### Clone `gencert`
```
git clone https://gitlab.cee.redhat.com/savsingh/gencert.git
```

## CSR Config
CSR config is enclosed in the project with predefined answers.
Consider changing `config` file as per your requirements before generating cert.

## Example
#### Generate CSR and Key
```
[savsingh@savitoj gencert]$ ./gencert savsingh.usersys.redhat.com config 
Generating a 4096 bit RSA private key
..++
..............................................................................................................................................................................................................................................................................................++
writing new private key to 'savsingh.usersys.redhat.com.key'
-----
Created savsingh.usersys.redhat.com.key
Created savsingh.usersys.redhat.com.csr
```
#### Generate Self Sign Certificate
```
[savsingh@savitoj gencert]$ ./gencert --selfsign savsingh.usersys.redhat.com config 
Generating a 4096 bit RSA private key
........++
..........................................................................++
writing new private key to 'savsingh.usersys.redhat.com.key'
-----
Created savsingh.usersys.redhat.com.key
Created savsingh.usersys.redhat.com.csr
Signature ok
subject=/C=US/ST=North Carolina/L=Raleigh/O=Red Hat, Inc./CN=savsingh.usersys.redhat.com
Getting Private key
Created savsingh.usersys.redhat.com.crt (self-signed)
```

## What's Next?
- Send `only CSR` generated to `Certificate Authority` to sign, Expect `CRT` and `CA Cert(s)` from `Certificate Authority`
- `No actions` required for `Self Sign certificate` generated
