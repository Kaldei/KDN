---
title: OPENSSL
summary: TLS/SSL and crypto library.
description: TLS/SSL and crypto library.
tags:
  - tls
---

# SSL Client

---

### Diag an SSL/TLS connection


 > 
 > **<font color=red>openssl s_client -connect</font> \[MY_HOST\]<font color=red>:</font>\[MY_PORT\]**</br>
 > Make an SSL/TLS client request.

# Generate Keys

---

### Generate RSA Key


 > 
 > **<font color=red>openssl genrsa -out</font> my-key.key <font color=red>4096</font>**</br>
 > Generate an RSA key (4096 bits for more robust than default 2048 bits).

 > 
 > **<font color=red>-aes256</font>**</br>
 > Gen a AES256 key.
 > To encrypt with passphrase (recommended only for root CA)?????????????

# Read Certificates

---

### Read Local Certificates


 > 
 > **<font color=red>openssl x509 -in</font> cert<font color=red>.pem -text</font>**</br>
 > Output certificate content as text.

 > 
 > **<font color=red>openssl req -in</font> cert<font color=red>.csr -text</font>**</br>
 > Output certificate content as text.

 > 
 > **<font color=red>-noout</font>**</br>
 > Do not outpout raw certificate at the end.

---

### Read Remote Certificates


 > 
 > **<font color=red>openssl s_client -showcerts -connect</font> \[MY_HOST\]<font color=red>:</font>\[MY_PORT\]**</br>
 > Return detail about  SSL/TLS connection and certificate chain.

# Generate Certificates

---

### Generate CA Certificate


 > 
 > **<font color=red>openssl genrsa -aes256 -out </font>ca.key 4096**</br>
 > Generate an RSA key.
 > 
 > **<font color=red>openssl req -new -x509 -sha256 -days</font> 3650 <font color=red>-key</font> ca.key <font color=red>-out</font> ca<font color=red>.pem</font>**</br>
 > Generate CA certificate with the given key (use `-x509` to self sign the CSR).

---

### Generate Server Certificate


 > 
 > **<font color=red>openssl genrsa -out </font>cert.key 4096**</br>
 > Generate an RSA key.
 > 
 > **<font color=red>openssl req -new -sha256 -key</font> cert.key <font color=red>-out</font> cert<font color=red>.csr</font>**</br>
 > Generate a certificate singing request with the given key.
 > 
 > **<font color=red>echo "subjectAltName=</font>DNS<font color=red>:</font>my-domain.tld<font color=red>,</font>IP<font color=red>:</font>10.0.0.1<font color=red>" ></font> sans.txt**</br>
 > Create a config file for SANs.
 > 
 > **<font color=red>openssl x509 -req -sha256 -days</font> 365 <font color=red>-in</font> cert<font color=red>.csr -CA</font> ca.<font color=red>pem -CAkey</font> ca<font color=red>.key -out</font> cert<font color=red>.pem -extfile</font> sans.txt**</br>
 > Create a certificate signed by CA and with a SAN config.

---

### Flags


 > 
 > **<font color=red>-subj "/C=</font>FR<font color=red>/ST=</font>Ile-de-France<font color=red>/L=</font>Paris<font color=red>/O=</font>MyOrg<font color=red>/OU=</font>MyUnit<font color=red>/CN=</font>my.domain<font color=red>"</font>**</br>
 > Specify information for the certificate in the command.

 > 
 > **<font color=red>-addext "subjectAltName=</font>DNS:my.alt.domain<font color=red>"</font>**</br>
 > Adding this with `req new` command does add the SAN to the request, but it does seem to be added to the final cert.</br>
 > The workaround of adding `<(printf "subjectAltName=DNS:my.alt.domain")` at the end of the command seem to work.

 > 
 > **<font color=red>-CAcreateserial</font>**</br>
 > No longer needed with OpenSSL 3 as it now generates a random serial numbers by default.
