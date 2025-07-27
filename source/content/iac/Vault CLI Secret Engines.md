---
title: Vault CLI Secret Engines
summary: A note on how to configure and interact with some Vault Secret Engines.
description: A note on how to configure and interact with some Secret Engines.
tags:
  - vault
---

# KV

---

### Enable (KV v1)


 > 
 > **<font color=red>vault secrets enable kv</font>**</br>
 > Enable KV v1 secret engine (default is KV v1).
 > 
 > **<font color=red>vault secrets enable kv -version=1</font>**</br>
 > Enable KV v1 secret engine.

 > 
 > **<font color=red>vault kv enable-versioning</font> my_engine_path**</br>
 > Enable versioning for a KV v1 Secret Engine (convert to KV v2).

---

### Enable (KV v2)


 > 
 > **<font color=red>vault secrets enable kv-v2</font>**</br>
 > Enable KV v2 secret engine.
 > 
 > **<font color=red>vault secrets enable kv -version=2</font>**</br>
 > Enable KV v2 secret engine.

---

### List


 > 
 > **<font color=red>vault kv list</font> my_kv_path**</br>
 > List secrets in a kv secret engine.

---

### Get


 > 
 > **<font color=red>vault kv get</font> my_secret**</br>
 > Read a secret.
 > 
 > **<font color=red>vault kv get -format=json</font> my_secret <font color=red>\| jq -r .data</font>**</br>
 > Read a secret and output in JSON.

 > 
 > **<font color=red>vault kv get -field=</font>foo my_secret**</br>
 > Read one field.
 > 
 > **<font color=red>vault kv get -format=json</font> my_secret <font color=red>\| jq -r .data.data.</font>foo**</br>
 > Read one field and output in JSON.

---

### Put


 > 
 > **<font color=red>vault kv put</font> my_secret key<font color=red>=</font>value**</br>
 > Create or replace a secret with one key value.
 > 
 > **<font color=red>vault kv put</font> my_credentials username<font color=red>=</font>myUser password<font color=red>=</font>myPass**</br>
 > Create or replace a new secret composed multiple key values.

---

### Patch (KV v2)


 > 
 > **<font color=red>vault kv patch</font> my_credentials password<font color=red>=</font>myNewPass**</br>
 > Create a new version by replacing only provided values (partial update) instead of replace all values like `kv put`.

---

### Rollback (KV v2)


 > 
 > **<font color=red>vault kv rollback -versions=</font>12 my_secret**</br>
 > Restore a non deleted version (create a new version with the values of the one to restore).

---

### Delete


 > 
 > **<font color=red>vault kv delete</font> my_secret**</br>
 > Permanently delete the secret.

---

### Delete (KV v2)


 > 
 > **<font color=red>vault kv delete -versions=</font>12 my_secret**</br>
 > Mark the version as deleted (soft delete).</br>
 > It can be restored with `vault kv undelete`.

---

### Undelete (KV v2)


 > 
 > **<font color=red>vault kv undelete -versions=</font>12 my_secret**</br>
 > Restore a version of a secret. Only works if secret was not destroyed (`destroyed` property set to `false`).

---

### Destroy (KV v2)


 > 
 > **<font color=red>vault kv destroy -versions=</font>12  my_secret**</br>
 > Permanently delete specified version(s) of a secret (cannot be recovered).

---

### Metadata (KV v2)


 > 
 > **<font color=red>vault kv metadata delete</font> my_secret**</br>
 > Permanently deletes the secret (thus all of it versions).

# Transit

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
 > Rotate the Key (create a new version).</br>
 > Old versions of the key will still exist (they are managed by `min_decryption_version`).

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
