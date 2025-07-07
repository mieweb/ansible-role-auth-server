# Ansible Role: mieweb_auth_app

This role installs and configures the MIEWEB Auth App, including Node.js, NGINX, and Cloudflared.

## Role Variables

| Variable                        | Default                                      | Description                                      |
|---------------------------------|----------------------------------------------|--------------------------------------------------|
| `root_url`                      | `http://localhost`                           | Application root URL                             |
| `mongo_url`                     | `mongodb://localhost:27017/mieweb_auth_app`  | MongoDB connection string                        |
| `ssl_cert_pem`                  | `CHANGEME: PEM-encoded certificate goes here`| PEM-encoded SSL certificate (set in inventory)   |
| `ssl_key_pem`                   | `CHANGEME: PEM-encoded private key goes here`| PEM-encoded SSL private key (set in inventory)   |
| `firebase_service_account_json` | *(none)*                                     | Firebase service account JSON (provide securely)  |
| `cloudflared_token`             | *(none)*                                     | Cloudflared service token (provide securely)      |

## Example Playbook

```yaml
- hosts: all
  become: yes
  roles:
    - role: mieweb.auth_server
      vars:
        firebase_service_account_json: "{{ vault_firebase_service_account_json }}"
        cloudflared_token: "{{ vault_cloudflared_token }}"
        ssl_cert_pem: "{{ vault_ssl_cert_pem }}"
        ssl_key_pem: "{{ vault_ssl_key_pem }}"
```

## How it works
- The role is modular: tasks are split into `nodejs.yml`, `meteor_app.yml`, `nginx.yml`, and `cloudflared.yml`.
- SSL cert/key are written from PEM variables to `/etc/ssl/nginx/<host>.crt` and `.key` (host is extracted from `root_url`).
- `/etc/hosts` is updated to map the app host to `127.0.0.1`.
- NGINX and Cloudflared are installed and configured.

## Notes
- You must provide the Firebase service account JSON and SSL certificates (PEM format) via Ansible variables or vault.
- The role will install all required dependencies and configure services.
- Do not override `ssl_cert` or `ssl_key` directly; use `root_url` and the role will handle the rest.
