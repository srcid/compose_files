# Cloudflare DNS over HTTPS

Using cloudflared to resolve dns queris using DoH.

## Testing it

Use `dig` to perform a DNS query.

```shell
dig @127.0.0.1 -p 5053 google.com
```