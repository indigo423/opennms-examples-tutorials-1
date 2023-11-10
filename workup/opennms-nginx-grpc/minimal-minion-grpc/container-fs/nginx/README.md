# public and private keys

A self signed certificate is provided here with a life of 5 years. 

You can regenerate these certifictes using the following instructions

## regenerating self signed certificate

see tutorial at https://www.humankode.com/ssl/create-a-selfsigned-certificate-for-nginx-in-5-minutes/

on a linux machine with openssl installed, edit a file localhost.conf 

```
sudo nano localhost.conf
```
and fill with the following - modify values as desired

```
[req]
default_bits       = 2048
default_keyfile    = localhost.key
distinguished_name = req_distinguished_name
req_extensions     = req_ext
x509_extensions    = v3_ca

[req_distinguished_name]
countryName                 = Country Name (2 letter code)
countryName_default         = US
stateOrProvinceName         = State or Province Name (full name)
stateOrProvinceName_default = New York
localityName                = Locality Name (eg, city)
localityName_default        = Rochester
organizationName            = Organization Name (eg, company)
organizationName_default    = localhost
organizationalUnitName      = organizationalunit
organizationalUnitName_default = Development
commonName                  = Common Name (e.g. server FQDN or YOUR name)
commonName_default          = localhost
commonName_max              = 64

[req_ext]
subjectAltName = @alt_names

[v3_ca]
subjectAltName = @alt_names

[alt_names]
DNS.1   = localhost
DNS.2   = 127.0.0.1
```

Then create public and private keys, in this case for 5 years validity

```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout localhost.key -out localhost.crt -config localhost.conf
```

copy `localhost.key` and  `localhost.crt` to this directory.


