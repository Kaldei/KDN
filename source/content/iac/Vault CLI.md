---
title: Vault CLI
summary: A note about the Vault CLI.
description: A note about the Vault CLI.
tags:
  - vault
---

# Basis

---

### Env Variables


 > 
 > **<font color=red>export VAULT_TOKEN=</font>hvs.xxxxxxxxxxxxxxxx**</br>
 > Set Token for Token Authentication Method.

 > 
 > **<font color=red>export VAULT_SKIP_VERIFY=true</font>**</br>
 > Skip TLS check.

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

# Tokens

---

### Explore


 > 
 > **<font color=red>vault list auth/</font>my_auth_method<font color=red>/accessors</font>**</br>
 > List tokens created with specified Auth Method.

 > 
 > **<font color=red>vault token lookup -accessor</font> \<token_accessor>**</br>
 > Return info about the token (type, TTL, max TTL ...).

---

### Revoke


 > 
 > **<font color=red>vault token revoke</font> \<token_id>**</br>
 > Revoke token.
 > 
 > **<font color=red>vault token revoke -accessor</font> \<token_accessor>**</br>
 > Revoke token using its accessor.

 > 
 > **<font color=red>vault token revoke -self</font>**</br>
 > Revoke current token.

 > 
 > **<font color=red>vault token revoke -mode-path auth/</font>my_auth_method**</br>
 > Revoke all tokens (and their children) created with specified auth method.

# Traceability

---

### Entity


 > 
 > **<font color=red>vault list identity/entity/id</font>**</br>
 > List entities.

 > 
 > **<font color=red>vault delete identity/entity/id/</font>f53c4994-8458-6b6c-8cff-eaf869c9aefc**</br>
 > Delete entity.

---

### Audit Device


 > 
 > **<font color=red>vault audit list</font>**</br>
 > List audit devices.

 > 
 > **<font color=red>vault audit enable file file_path=</font>/var/log/vault_audit.log**</br>
 > Create an audit device (the user running Vault has to be able to write to the given path). 

 > 
 > **<font color=red>vault audit disable</font> file**</br>
 > Disable specified audit device.

 > 
 > **<font color=red>vault write sys/audit-hash/file input="</font>P@ssword!<font color=red>"</font>**</br>
 > Compute the hash for a given input (can be used to check hashed values in audit file). Warning: only admin should be able to write in `sys/audit-hash/file`.

# Access Control

---

### Lease


 > 
 > **<font color=red>vault lease revoke </font> aws/creds/myRole/my_lease_id**</br>
 > Revoke specified lease.
 > 
 > **<font color=red>vault lease revoke -prefix</font> aws/**</br>
 > Revoke all leases under the specified prefix.

---

### Policy


 > 
 > **<font color=red>vault policy list</font>**</br>
 > List policies.
 > 
 > **<font color=red>vault policy read</font> my-policy**</br>
 > Read policy content.

 > 
 > **<font color=red>vault policy write</font> my-policy my-policy<font color=red>.hcl</font>**</br>
 > Create a policy from local file.

 > 
 > **<font color=red>vault token capabilities</font> hvs.XXXXXXXXXXXX /transit/encrypt/my_key**</br>
 > Check capabilities of a token for the given path (output example: `update`).

---

### Namespaces (Enterprise)


 > 
 > **<font color=red>vault namespace list</font>**</br>
 > List namespaces.
 > 
 > **<font color=red>vault namespace create</font> my-namespace**</br>
 > Create namespace.
 > 
 > **<font color=red>vault namespace delete</font> my-namespace**</br>
 > Delete namespace.

 > 
 > **<font color=red>vault secrets list -namespace=</font>my_namespace**</br>
 > Use a namespace in a command.

# Authentication Methods

---

### Basis


 > 
 > **<font color=red>vault auth list</font>**</br>
 > List authentication backends enabled.

 > 
 > **<font color=red>vault auth enable</font> aws**</br>
 > Enable an authentication backend.

---

### Token


 > 
 > **<font color=red>vault token create -policy=</font>my_policy <font color=red>-ttl=</font>30m**</br>
 > Create a token with a specified Policy and TTL.

 > 
 > **<font color=red>vault token renew</font> myToken**</br>
 > Renew a token.

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

---

### AppRole


 > 
 > **<font color=red>vault auth enable approle</font>**</br>
 > Enable AppRole.

 > 
 > **<font color=red>vault write auth/approle/role/</font>my-role \ <font color=red>token_policies="</font>my-policy<font color=red>"</font>**</br>
 > Create an AppRole Role with a Policy.

 > 
 > **<font color=red>vault read auth/approle/role/</font>my-role<font color=red>/role-id</font>**</br>
 > Retrieve RoleId.
 > 
 > **<font color=red>vault write -f auth/approle/role/</font>my-role<font color=red>/secret-id</font>**</br>
 > Retrieve SecretId (`-f` because `write` operation without any data).

 > 
 > **<font color=red>vault write auth/approle/login role_id="</font>$ROLE_ID<font color=red>"</font> <font color=red>secret_id="</font>$SECRET_ID<font color=red>"</font>**</br>
 > Login using AppRole.

# Secret Engines

---

### List


 > 
 > **<font color=red>vault secrets list</font>**</br>
 > Return info about secret engines.
 > 
 > **<font color=red>vault secrets list -detailed</font>**</br>
 > Return more info about secret engines (e.g. KV version).

---

### Enable


 > 
 > **<font color=red>vault secrets enable -path=</font>my_secret_engine_path <font color=red>kv</font>**</br>
 > Create a new Key Value (KV) secrets engine.

---

### Modify


 > 
 > **<font color=red>vault secrets move</font> my/old/path my/new/path**</br>
 > Change the path of the Secret Engine.

 > 
 > **<font color=red>vault secrets tune</font> -default-lease-ttl=12h**</br>
 > Change the configuration of the Secret Engine.

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

# Operator

---

### Regenerate Root Token


 > 
 > **<font color=red>vault operator generate-root -generate-otp</font>**</br>
 > Generate an OTP for the `generate-root` command.

 > 
 > **<font color=red>vault operator generate-root -init -otp=</font>\<otp_token>**</br>
 > Initialize Root Token Generation. Give the generated nonce to the Recovery Keys holders.

 > 
 > **<font color=red>vault operator generate-root -nonce=</font>\<request_nonce>**</br>
 > Validate the request with every one that has a Recovery Keys until quorum is reached. This will return the encoded token.

 > 
 > **<font color=red>vault operator generate-root -decode=</font>\<encoded_token> <font color=red>-otp=</font>\<otp_token>**</br>
 > Decode the newly generated Root Token.

---

### ReKey (Regenerate Unseal Keys)


 > 
 > **<font color=red>vault operator rekey -init -key-shares=</font>3 <font color=red>-key-threshold=</font>2**</br>
 > Initialize request for ReKey.
 > 
 > **<font color=red>vault operator rekey -nonce=</font>\<request_nonce>**</br>
 > Validate the request with Useal Keys until quorum is reached. This will output new Unseal.

 > 
 > **<font color=red>vault operator rekey -target=recovery -init -key-shares=</font>3 <font color=red>-key-threshold=</font>2**</br>
 > Initialize request for ReKey with Recovery Key mode (Auto Unseal enabled).
 > 
 > **<font color=red>vault operator rekey -target=recovery -nonce=</font>\<request_nonce>**</br>
 > Validate the request with Recovery Keys until quorum is reached. This will output new Unseal.

---

### Rotate Encryption Keys


 > 
 > **<font color=red>vault operator rotate</font>**</br>
 > Vault automatically rotate the Encryption Key.

# Raft

---

### Cluster


 > 
 > **<font color=red>vault operator raft list-peers</font>**</br>
 > List Raft members.

 > 
 > **<font color=red>vault operator raft autopilot state</font>**</br>
 > Show current cluster autopilot state.
 > 
 > **<font color=red>vault operator raft autopilot get-config</font>**</br>
 > Show autopilot config.

---

### Snapshot


 > 
 > **<font color=red>vault operator raft snapshot save</font> backup.snap**</br>
 > Create a Snapshot.
 > 
 > **<font color=red>vault operator raft snapshot restore -force</font> backup.snap**</br>
 > Restore Snapshot from local file (copy the Snapshot file on the machine to restore). 
 > `-force` option is required here since the Auto-Unseal or Shamir keys will not be consistent with the snapshot data (snapshot from a different cluster).
 > https://developer.hashicorp.com/vault/tutorials/standard-procedures/sop-restore

---

### Snapshot Auto (Enterprise)


 > 
 > **<font color=red>vault list /sys/storage/raft/snapshot-auto/config</font>**</br>
 > List Auto Snapshot configs.
 > 
 > **<font color=red>vault read /sys/storage/raft/snapshot-auto/config/</font>my-auto-snapshot-config**</br>
 > Check specified Auto Snapshot config.

# Replication

---

### Basis


 > 
 > **<font color=red>vault read sys/replication/status</font>**</br>
 > Check replication status (DR and Performance).

---

### Disaster Recovery

https://developer.hashicorp.com/vault/tutorials/enterprise/disaster-recovery

 > 
 > **<font color=red>vault read sys/replication/dr/status</font>**</br>
 > Check DR replication status.

 > 
 > **<font color=red>vault write -f sys/replication/dr/primary/enable</font>**</br>
 > Enable DR replication as Primary.
 > 
 > **<font color=red>vault write sys/replication/dr/primary/secondary-token id=</font>dr-secondary**</br>
 > Create a token for a Secondary cluster.
 > 
 > **<font color=red>vault write sys/replication/dr/secondary/enable token=</font>DR_SECONDARY_TOKEN**</br>
 > Enable DR replication as Secondary.

---

### Performance

https://developer.hashicorp.com/vault/tutorials/enterprise/performance-replication#configure-the-secondary-cluster

 > 
 > **<font color=red>vault read sys/replication/performance/status</font>**</br>
 > Check Performance replication status.

 > 
 > **<font color=red>vault write -f sys/replication/performance/primary/enable</font>**</br>
 > Enable Performance replication as Primary.
 > 
 > **<font color=red>vault write sys/replication/performance/primary/secondary-token id=</font>perf-secondary**</br>
 > Create a token for a Secondary cluster.
 > 
 > **<font color=red>vault write sys/replication/performance/secondary/enable token=</font>PERF_SECONDARY_TOKEN**</br>
 > Enable Performance replication as Secondary.

# Agent

---

### Basis


 > 
 > **<font color=red>vault agent generate-config -type="</font>env-template<font color=red>" -exec="</font>./my_script.sh<font color=red>" -path="</font>secret/my_secret<font color=red>"</font> agent-config<font color=red>.hcl</font>**</br>
 > Generate a configuration file for an agent.

 > 
 > **<font color=red>vault agent -config=</font>agent-config<font color=red>.hcl</font>**</br>
 > Run an agent.
