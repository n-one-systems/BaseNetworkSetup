# Playbooks

Sample playbooks for network performance testing will be placed here.

## Available Samples

- `netperf_fullmesh.yml` - uses the `sample_inventory.yaml` inventory and
  deploys a full mesh of iperf3 server and client instances so that every host
  in the `servers` group tests connectivity with all other hosts.
- `netperf_single_client.yml` - designates one host as the client and runs
  iperf3 tests against all other hosts.

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
