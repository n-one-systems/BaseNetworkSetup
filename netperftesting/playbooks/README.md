# Playbooks

Sample playbooks for network performance testing will be placed here.

## Available Samples

- `netperf_fullmesh.yml` - uses the `sample_inventory.yaml` inventory and
  deploys a full mesh of iperf3 server and client instances so that every host
  in the `servers` group tests connectivity with all other hosts.
