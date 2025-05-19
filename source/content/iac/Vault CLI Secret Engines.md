---
title: Vault CLI Secret Engines
summary: A note on how to configure and interact with some Vault Secret Engines.
description: A note on how to configure and interact with some Secret Engines.
tags:
  - vault
---

# Secret Engine KV

---

### List


 > 
 > **<font color=red>vault kv list kv</font>**</br>
 > List secrets in a kv secret engine.

---

### Get


 > 
 > **<font color=red>vault kv get -mount=</font>my_engine_path my_secret**</br>
 > Read a secret.
 > 
 > **<font color=red>vault kv get -mount=</font>my_engine_path <font color=red>-format=json</font> my_secret <font color=red>\| jq -r .data</font>**</br>
 > Read a secret and output in JSON.

 > 
 > **<font color=red>vault kv get -mount=</font>my_engine_path <font color=red>-field=</font>foo my_secret**</br>
 > Read one field.
 > 
 > **<font color=red>vault kv get -mount=</font>my_engine_path <font color=red>-format=json</font> my_secret <font color=red>\| jq -r .data.data.</font>foo**</br>
 > Read one field and output in JSON.

---

### Put


 > 
 > **<font color=red>vault kv put -mount=</font>my_engine_path my_secret key<font color=red>=</font>value**</br>
 > Create a secret (or replace pre-existing).

 > 
 > **<font color=red>vault kv put -mount=</font>my_engine_path my_credentials username<font color=red>=</font>myUser password<font color=red>=</font>myPass**</br>
 > Create a new secret composed of credentials.

---

### Delete


 > 
 > **<font color=red>vault kv delete -mount=</font>my_engine_path <font color=red>-versions=</font>2 my_secret**</br>
 > In KV v1, permanently delete specified the secret.
 > In KV v2, mark the secret as deleted. The secret is still readable when specifying the version explicitly (it can be restored with `vault kv undelete`).

---

### KV v2 Specific


 > 
 > **<font color=red>vault kv undelete -mount=</font>my_engine_path <font color=red>-versions=</font>2 my_secret**</br>
 > Recover password. Only works if `destroyed` parameter is set to `false`.

 > 
 > **<font color=red>vault kv destroy -mount=</font>my_engine_path <font color=red>-versions=</font>1  my_secret**</br>
 > Permanently delete specified version(s) of a secret (cannot be recovered).
 > 
 > **<font color=red>vault kv metadata delete -mount=</font>my_engine_path my_secret**</br>
 > Permanently deletes the secret (thus all of it versions).

 > 
 > **<font color=red>vault kv enable-versioning</font> my_engine_path**</br>
 > Enable versioning for a KV v1 Secret Engine (convert to v2).

# Secret Engine Transit

---

### Enable


 > 
 > **<font color=red>vault secrets enable transit</font>**</br>
 > Enable Transit secret engine.

---

### Keys


 > 
 > **<font color=red>vault list</font> transit<font color=red>/keys</font>**</br>
 > List Keys in Transit engine. 

 > 
 > **<font color=red>vault write -f</font> transit<font color=red>/keys/</font>my-key**</br>
 > Create a new Key.
 > 
 > **<font color=red>vault write -f</font> transit<font color=red>/keys/</font>my_key<font color=red>/rotate</font>**</br>
 > Rotate the Key (create a new version). Old versions of the key will still exist (they are managed by `min_decryption_version`).

---

### Encryption


 > 
 > **<font color=red>vault write</font> transit<font color=red>/encrypt/</font>my_key <font color=red>plaintext=$(echo "</font>my secret data<font color=red>" | base64)</font>**</br>
 > Encrypt data.
 > 
 > **<font color=red>vault write -field=plaintext</font> transit<font color=red>/decrypt/</font>my_key <font color=red>ciphertext=</font>vault:v1:qRuV... <font color=red>\| base64 -d</font>**</br>
 > Decrypt data (`-field=plaintext` to only get the base64 decrypted data).

 > 
 > **<font color=red>vault write</font> transit<font color=red>/rewrap/</font>my-key <font color=red>ciphertext=</font>vault:v1:8SDd...**</br>
 > Decrypt then re-encrypt data with a newer version of the key.
