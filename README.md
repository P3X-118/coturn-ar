# coturn-ar

SGC Ansible role for [coturn](https://github.com/coturn/coturn), a TURN/STUN
server for WebRTC NAT traversal.

Runs the upstream `coturn/coturn` Docker image as a systemd-managed service in
host-network mode (required for the wide UDP media-port range).

Designed to be consumed by the SGC master playbook. See `defaults/main.yml`
for the full variable surface.

## Required variables

- `coturn_realm` — TURN realm (e.g. `meet.sgc.ai`).
- `coturn_external_ip` — public IPv4 advertised as the relay address.
- `coturn_user_name` / `coturn_user_password` — long-term credential.

## Ports

- UDP/TCP `coturn_listening_port` (default 3478) — STUN + TURN.
- TCP `coturn_tls_listening_port` (default 5349) — TURN-TLS, opt-in via
  `coturn_tls_enabled: true`.
- UDP `coturn_min_port`–`coturn_max_port` (default 49152–65535) — media relay.

Open these inbound on the host's network/firewall as appropriate.
