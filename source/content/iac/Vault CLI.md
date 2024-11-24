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

# Secret Engine

---

### List


 > 
 > **<font color=red>vault secrets list</font>**</br>
 > Return info about secret engines.

---

### Enable


 > 
 > **<font color=red>vault secrets enable -path=</font>my-secret-engine <font color=red>kv</font>**</br>
 > Create a new Key Value (KV) secrets engine.

# Secret Management

---

### Put


 > 
 > **<font color=red>vault kv put -mount=</font>my-secret-engine hello mySecret=world**</br>
 > Create a secret (or replace pre-existing) at path `hello` with value `world`.

 > 
 > **<font color=red>vault kv put -mount=</font>my-secret-engine myCredentials username=myUsername password=myPassword**</br>
 > Create a new secret composed of credentials.

---

### Read


 > 
 > **<font color=red>vault kv get -mount=</font>my-secret-engine hello**</br>
 > Read a secret.
 > 
 > **<font color=red>vault kv get -mount=</font>my-secret-engine <font color=red>-format=json</font> hello <font color=red>\| jq -r .data</font>**</br>
 > Read a secret and output in JSON.

 > 
 > **<font color=red>vault kv get -mount=</font>my-secret-engine <font color=red>-field=</font>foo hello**</br>
 > Read one field.
 > 
 > **<font color=red>vault kv get -mount=</font>my-secret-engine <font color=red>-format=json</font> hello <font color=red>\| jq -r .data.data.</font>foo**</br>
 > Read one field and output in JSON.

---

### Delete


 > 
 > **<font color=red>vault kv delete -mount=</font>my-secret-engine hello**</br>
 > Delete a secret.

 > 
 > **<font color=red>vault kv undelete -mount=</font>my-secret-engine <font color=red>-versions=</font>2 hello**</br>
 > Recover password. Only works if `destroyed` parameter is set to `false` (means that it is possible to recover deleted data if the deletion was unintentional).
