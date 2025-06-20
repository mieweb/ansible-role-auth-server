---
# README.md
# Ansible Role: mieweb_auth_app

This role installs and configures the MIEWEB Auth App, including Node.js, MongoDB, NGINX, and Cloudflared.

## Role Variables

- `node_version`: Node.js version (default: v20.18.0)
- `root_url`: Application root URL
- `bind_ip`: Bind IP for the app
- `port`: App port
- `mongo_url`: MongoDB connection string
- `ssl_cert`: Path to SSL certificate for NGINX
- `ssl_key`: Path to SSL key for NGINX
- `firebase_service_account_json`: Firebase service account JSON (should be provided securely)
- `cloudflared_token`: Cloudflared service token (should be provided securely)

## Usage

```yaml
- hosts: all
  become: yes
  roles:
    - role: ansible-role-auth-server
      vars:
        firebase_service_account_json: "{{ vault_firebase_service_account_json }}"
        cloudflared_token: "{{ vault_cloudflared_token }}"
```

## Notes
- You must provide the Firebase service account JSON and SSL certificates.
- The role will install all required dependencies and configure services.
