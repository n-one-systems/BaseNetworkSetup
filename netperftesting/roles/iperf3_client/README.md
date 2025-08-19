# iperf3_client role

Installs iperf3 and provides a systemd template unit (`iperf3-client@.service`)
to run multiple iperf3 client instances with per-instance configuration files.
Each configuration file defines `TARGET_IP`, `TARGET_PORT`, `PROTOCOL`, and
optional `EXTRA_ARGS` variables used by the service to connect to different
servers, ports, and protocols.

## Variables

- `iperf3_client_instances`: List of client service definitions. Each item
  should include:
  - `name`: Instance name (used for configuration file and systemd unit)
  - `target`: Target host IP or name
  - `port`: Target port or `default+<offset>` to offset from the default
  - `protocol`: `tcp` (default) or `udp`
  - `bandwidth` (optional): Bandwidth for UDP tests
  - `extra_args` (optional): Additional iperf3 arguments

Example:

```yaml
iperf3_client_instances:
  - name: test_network1
    target: 192.168.10.11
    port: default+1
    protocol: udp
    bandwidth: 0
  - name: test_network2
    target: 192.168.10.12
    port: default+2
```
