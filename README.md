# Renew HashiCorp Vault
An Ansible Playbook to renew a HashiCorp Vault token using the REST API

## Usage

1) Create a vault.yml file to pass the extra vars to the playbook. The vault.yml file should look like this:

```yaml
vault_address: "https://vault.example.com:8200"
vault_token: "s.1234567890"
```

2) Encrypt the vault.yml file using ansible-vault:

```bash
ansible-vault encrypt vault.yml
```

You can also pass the extra vars directly to the playbook using the -e flag. Or if running in AAP, you can attach them to the job template.

3) Run the playbook:

```bash
ansible-playbook renew-vault-token.yml -e @vault.yml --ask-vault-pass
```
