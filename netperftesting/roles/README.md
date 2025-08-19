# Roles

Ansible roles for network performance testing:

- **iperf3_server**: Installs iperf3 and provides a systemd template
  to run multiple iperf3 server instances on different ports.
- **iperf3_server_cleanup**: Removes iperf3 server package, service units, and logs.
- **iperf3_client**: Installs iperf3 and provides a systemd template to
  run multiple iperf3 clients with per-instance configuration files.
- **iperf3_client_cleanup**: Removes iperf3 client configuration, logs, and package.
