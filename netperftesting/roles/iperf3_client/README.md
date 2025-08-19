# iperf3_client role

Installs iperf3 and provides a systemd template unit (`iperf3-client@.service`)
to run multiple iperf3 client instances with per-instance configuration files.
Each run logs to `journald` and stores its JSON results in a per-connection file
for later analysis. Each configuration file defines `TARGET_IP`, `TARGET_PORT`,
`PROTOCOL`, and optional `EXTRA_ARGS` variables used by the service to connect
to different servers, ports, and protocols. All services execute as a minimal
`iperf3` system user; the role ensures this user exists and that the log
directory is owned by it.

## Variables

- `iperf3_client_instances`: List of client service definitions. Each item
  should include:
  - `name`: Instance name (used for configuration file and systemd unit)
  - `target`: Target host IP or name
  - `port`: Target port or `default+<offset>` to offset from the default
  - `protocol`: `tcp` (default) or `udp`
  - `bandwidth` (optional): Bandwidth for UDP tests
  - `extra_args` (optional): Additional iperf3 arguments

- `iperf3_client_log_dir`: Directory where JSON output from each client run
  is stored. Log files are named `<client>-to-<instance>.json` where
  `<client>` is the Ansible inventory hostname and `<instance>` is the service
  instance name. Defaults to `/var/log/iperf3-client`.

- `iperf3_client_auto_start`: Whether client services should be started
  automatically after configuration. Defaults to `true`.
- `iperf3_client_auto_enable`: Whether client services should be enabled to
  start at boot. Defaults to `true`.

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
