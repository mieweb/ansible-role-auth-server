# Ansible Role: mieweb_auth_app

This role installs and configures the MIEWEB Auth App, including Node.js, NGINX, and Cloudflared.

## Role Variables

| Variable                        | Default                                      | Description                                      |
|---------------------------------|----------------------------------------------|--------------------------------------------------|
| `root_url`                      | `http://localhost`                           | Application root URL                             |
| `mongo_url`                     | `mongodb://localhost:27017/mieweb_auth_app`  | MongoDB connection string                        |
| `ssl_cert`                      | `/etc/ssl/nginx/example.crt`                 | Path to SSL certificate for NGINX                |
| `ssl_key`                       | `/etc/ssl/nginx/example.key`                 | Path to SSL key for NGINX                        |
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
```

## Notes
- You must provide the Firebase service account JSON and SSL certificates.
- The role will install all required dependencies and configure services.
