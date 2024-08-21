# Renew HashiCorp Vault Token
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
ansible-playbook renew.yml -e @vault.yml --ask-vault-pass
```

## Usage in AAP
To run on Ansible Automation Platform without a custom credential type:
1) Create a new job template with `renew.yml` as the playbook
2) Add `vault_address` as an extra var and set the default value appropriately
3) Add a survey question (type: password) that assigns it's value to `vault_token` and set the default value appropriately (this will ensure the token is encrypted)
4) Set a schedule for the job template to run on the desired interval

Alternatively, you can create a custom credential type to store the vault token and address. This will allow you to avoid using a survey and will allow you to store the token securely in the AAP credential store. Have the credential type contain extra vars for `vault_address` and `vault_token` and ensure the token value is encrypted. Then, create a new credential with the custom credential type and assign it to the job template.
