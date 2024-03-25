# Tailscale

Tailscale VPN client with docker.

## Running without compose

```shell
docker run -name ts -d -e TS_AUTHKEY="${AUTHKEY}" -e TS_HOSTNAME="rasp" -e TS_USERSPACE=false -e TS_STATE_DIR="/var/lib/tailscale" -e TS_EXTRA_ARGS="--advertise-exit-node" -v /var/run/dbus/system_bus_socket:/var/run/dbus/system_bus_socket -v tailscale_var-lib:/var/lib --device /dev/net/tun:/dev/net/tun --network host --restart unless-stopped --cap-add NET_RAW --cap-add NET_ADMIN --cap-add SYS_MODULE tailscale/tailscale:latest
```

## Variables

```yaml
TS_HOSTNAME: hal001 # Otherwise it will take the random container hostname name
TS_USERSPACE: false # Force use of kernel network.
TS_STATE_DIR: /var/lib/tailscale # Save the daemon state on the same volume that tailscale other data. 
TS_AUTHKEY: ${AUTHKEY} # Your tailscale authorization key.
TS_ROUTES: "192.168.0.0/24" # Local route you want to be exposed on the tailnet.
TS_EXTRA_ARGS: 
  "--advertise-exit-node" # Remove if you don't want it as an exit node.
  " --accept-routes" # Remove if you don't want to routes from tailnet. 
  "--exit-node=${EXIT_NODE_IP}" # Make use of exit node of the respctive IP.
  "--exit-node-allow-lan-access=true" # Make your LAN accessible to the exit node.
```

## Problems

I wasn't able it as exit node. On the admin cosole appears to be OK, but it just don't work. I think it must be a capability issue, but I'm not sure. I'm going to test with those below.

```yaml
cap_add:
  ...
  - NET_BIND_SERVICE
  - NET_BROADCAST
  - SYS_MODULE
  - SYS_ADMIN
```