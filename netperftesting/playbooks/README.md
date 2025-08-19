# Playbooks

Sample playbooks for network performance testing will be placed here.

## Available Samples

- `netperf_fullmesh.yml` - uses the `sample_inventory.yaml` inventory and
  deploys a full mesh of iperf3 server and client instances so that every host
  in the `servers` group tests connectivity with all other hosts.
- `netperf_single_client.yml` - designates one host as the client and runs
  iperf3 tests against all other hosts.
- `netperf_single_server.yml` - designates one host as the server and runs
  iperf3 tests from all other hosts.
- `netperf_stress.yml` - launches multiple concurrent UDP streams between all
  hosts for high-stress testing.

### `netperf_single_client.yml`

This playbook starts an `iperf3_server` instance on every host except the one
specified by the `client_host` variable. The designated client then connects to
each server using the `iperf3_client` role.

#### Inventory example

```yaml
all:
  vars:
    client_host: deb-srv-01
  children:
    test_hosts:
      hosts:
        deb-srv-01:
          test_ip: 192.168.254.11/24
        deb-srv-02:
          test_ip: 192.168.254.12/24
        deb-srv-03:
          test_ip: 192.168.254.13/24
```

#### Usage

Run a TCP test (default protocol):

```bash
ansible-playbook -i inventory.yaml netperftesting/playbooks/netperf_single_client.yml
```

Run a UDP test with an optional bandwidth limit:

```bash
ansible-playbook -i inventory.yaml netperftesting/playbooks/netperf_single_client.yml \
  -e "protocol=udp bandwidth=100M"
```

### `netperf_single_server.yml`

This playbook starts an `iperf3_server` instance on the host specified by the
`server_host` variable. All other hosts connect to the designated server using
the `iperf3_client` role.

#### Inventory example

```yaml
all:
  vars:
    server_host: deb-srv-01
  children:
    test_hosts:
      hosts:
        deb-srv-01:
          test_ip: 192.168.254.11/24
        deb-srv-02:
          test_ip: 192.168.254.12/24
        deb-srv-03:
          test_ip: 192.168.254.13/24
```

#### Usage

Run a TCP test (default protocol):

```bash
ansible-playbook -i inventory.yaml netperftesting/playbooks/netperf_single_server.yml
```

Run a UDP test with an optional bandwidth limit:

```bash
ansible-playbook -i inventory.yaml netperftesting/playbooks/netperf_single_server.yml \
  -e "protocol=udp bandwidth=100M"
```

### `netperf_stress.yml`

This playbook starts `connections_per_pair` iperf3 server instances on each
host for every other host and launches the same number of UDP clients toward
each peer. Clients run with unlimited bandwidth (`-b 0`) for
`test_duration` seconds (default `600`) to maximize network load.

#### Usage

Run with defaults:

```bash
ansible-playbook -i inventory.yaml netperftesting/playbooks/netperf_stress.yml
```

Specify five connections per pair for 300-second runs:

```bash
ansible-playbook -i inventory.yaml netperftesting/playbooks/netperf_stress.yml \
  -e "connections_per_pair=5 test_duration=300"
```
