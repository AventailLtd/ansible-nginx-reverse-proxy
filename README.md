# Nginx reverse proxy
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
```
