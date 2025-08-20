# iperf3_server role

Installs iperf3 and provides a systemd template unit (`iperf3@.service`)
to allow multiple iperf3 server instances to run on different ports. Services
run under a dedicated `iperf3` system user with no shell for minimal
privileges.

## Variables

- `iperf_base_prefix`: Optional string appended to the base `iperf3` name.
  When set, systemd services and log identifiers are prefixed as
  `iperf3<prefix>` to avoid collisions. Defaults to empty.
- `iperf3_server_instances`: List of ports to run server instances on.
  Defaults to `[]`.
