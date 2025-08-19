# iperf3_server role

Installs iperf3 and provides a systemd template unit (`iperf3@.service`)
to allow multiple iperf3 server instances to run on different ports.

## Variables

- `iperf3_server_instances`: List of ports to run server instances on.
  Defaults to `[]`.
