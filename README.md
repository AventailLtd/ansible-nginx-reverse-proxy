# Nginx reverse proxy Ansible role

Nginx reverse proxy and load balancer Ansible role with Let's Encrypt. 
 
## Example

```yaml
# List of sites to reverse proxy
nginx_reverse_proxy_sites:
  # Domain name
  example.com:
    client_max_body_size: "256M"
    proxy_read_timeout: "360"
    # List of server_name aliases
    domains:
      - example.com
      - www.example.com
    # List of Upstreams
    upstreams:
      - { backend_address: 127.0.0.1, backend_port: 80 }
      - { backend_address: 127.0.0.1, backend_port: 8080, options: ['backup'] }
    # Set to True if you want https
    ssl: true
    # Set HSTS header with max-age defined
    hsts_max_age: 63072000
    # Set to True if you want use letsencrypt
    letsencrypt: true
    # Set email for letencrypt cert
    letsencrypt_email: ""
    # Auto redirect http site to https
    redirect_http: true
    extra_configs:
      - "proxy_set_header X-Forwarded-Host $host;"
      - "proxy_set_header X-Forwarded-Proto $scheme;"
```

## Add new domain alternative

If you add a new domain alternative, the cert content must be regenerated:
 - Comment "creates=" line from "Generate certs" task. (https://github.com/AventailLtd/ansible-nginx-reverse-proxy/blob/main/tasks/letsencrypt.yml#L53)
