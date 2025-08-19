# iperf3_cleanup

Stops iperf3 client and server services, removes configuration and logs,
deletes systemd templates, and optionally uninstalls iperf3.

The role reuses the same variables as the `iperf3_client` and
`iperf3_server` roles so the same values can be supplied for both setup
and cleanup.

## Role Variables
- `iperf3_cleanup_remove_package` (bool, default: `true`): whether to remove the iperf3 package.
- `iperf3_client_package` (string, default: `iperf3`): package name to remove.
- `iperf3_client_conf_dir` (string, default: `/etc/iperf3-client`): client configuration directory.
- `iperf3_client_log_dir` (string, default: `/var/log/iperf3-client`): client log directory.
- `iperf3_server_log_dir` (string, default: `/var/log/iperf3`): server log directory.
