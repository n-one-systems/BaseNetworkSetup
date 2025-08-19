# Roles

Ansible roles for network performance testing:

- **iperf3_server**: Installs iperf3 and provides a systemd template
  to run multiple iperf3 server instances on different ports.
- **iperf3_client**: Installs iperf3 and provides a systemd template to
  run multiple iperf3 clients with per-instance configuration files.
- **iperf3_cleanup**: Stops iperf3 services, removes configuration and logs,
  deletes systemd templates, and optionally uninstalls iperf3.
