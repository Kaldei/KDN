---
title: Vault CLI
summary: A note about the Vault CLI.
description: A note about the Vault CLI.
tags:
  - vault
---

# Initialization

---

### Check Status


 > 
 > **<font color=red>vault status</font>**</br>
 > Check if server is running.

---

### Initialize and Unseal Vault


 > 
 > **<font color=red>vault operator init</font>**</br>
 > Initialize vault.

 > 
 > **<font color=red>vault operator unseal</font>**</br>
 > Ask for an unseal keys to unlock the vault (it unlocks when the required number of unseal keys are given).

---

### Login


 > 
 > **<font color=red>vault login</font>**</br>
 > Login to the server.

# Authentication Methods

---

### UserPass


 > 
 > **<font color=red>vault auth enable userpass</font>**</br>
 > Enable UserPass Auth Method.

 > 
 > **<font color=red>vault list auth/userpass/users/</font>**</br>
 > List created users
 > 
 > **<font color=red>vault write auth/userpass/users/</font>my_user <font color=red>password="</font>my_pass<font color=red>"</font>**</br>
 > Create a password for user "my_user".

 > 
 > **<font color=red>vault login -method=userpass username=</font>my_user <font color=red>password="</font>my_pass<font color=red>"</font>**</br>
 > Login to Vault using UserPass Auth Method.

# Secret Engines

---

### List


 > 
 > **<font color=red>vault secrets list</font>**</br>
 > Return info about secret engines.

---

### Enable


 > 
 > **<font color=red>vault secrets enable -path=</font>my_secret_engine_path <font color=red>kv</font>**</br>
 > Create a new Key Value (KV) secrets engine.

# KV Secret Engine

---

### Put


 > 
 > **<font color=red>vault kv put -mount=</font>my_secret_engine_path my_secret key<font color=red>=</font>value**</br>
 > Create a secret (or replace pre-existing).

 > 
 > **<font color=red>vault kv put -mount=</font>my_secret_engine_path my_credentials username<font color=red>=</font>myUser password<font color=red>=</font>myPass**</br>
 > Create a new secret composed of credentials.

---

### Read


 > 
 > **<font color=red>vault kv get -mount=</font>my_secret_engine_path my_secret**</br>
 > Read a secret.
 > 
 > **<font color=red>vault kv get -mount=</font>my_secret_engine_path <font color=red>-format=json</font> my_secret <font color=red>\| jq -r .data</font>**</br>
 > Read a secret and output in JSON.

 > 
 > **<font color=red>vault kv get -mount=</font>my_secret_engine_path <font color=red>-field=</font>foo my_secret**</br>
 > Read one field.
 > 
 > **<font color=red>vault kv get -mount=</font>my_secret_engine_path <font color=red>-format=json</font> my_secret <font color=red>\| jq -r .data.data.</font>foo**</br>
 > Read one field and output in JSON.

---

### Delete


 > 
 > **<font color=red>vault kv delete -mount=</font>my_secret_engine_path my_secret**</br>
 > Mark the secret as deleted (the secret is still readable when specifying the version explicitly).

 > 
 > **<font color=red>vault kv undelete -mount=</font>my_secret_engine_path <font color=red>-versions=</font>2 my_secret**</br>
 > Recover password. Only works if `destroyed` parameter is set to `false` (means that it is possible to recover deleted data if the deletion was unintentional).

---

### Destroy


 > 
 > **<font color=red>vault kv destroy -mount=</font>my_secret_engine_path <font color=red>-versions=</font>1  my_secret**</br>
 > Permanently delete version of a secret.
