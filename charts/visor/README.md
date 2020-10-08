# Sentinel Visor Helm Chart

This helm chart deploys Sentinel Visor.

## Dependencies

### Lotus

A [lotus](https://github.com/filecoin-project/lotus) daemon must be running with its' API exposed for Visor to consume.
This chart comes preconfigured to work in tandem with the [lotus-fullnode](https://github.com/filecoin-project/helm-charts/charts/lotus-fullnode) helm chart.


#### Secrets

Assumes a Kuberntes Secret named `{{ .Release.Name }}-jwt-secrets` with the following keys

* `jwt-ro-privs-token`: a JWT token generated by lotus node, with a minimum of read-only access

#### Service

Assumes a Kubernetes Service is available mapping to the lotus API
Can be configured with value `lotusAPIMultiaddr`
If value unset, uses default multiaddr `/dns/{{ .Release.Name }}-lotus-daemon.{{ .Release.Namespace }}.svc.cluster.local/tcp/1234`

### Redis

Redis is required to be available with no password configured
Can be configured with value `redisAddress`
If value unset, uses default address of `{{ .Release.Name }}-redis-master.{{ .Release.Namespace }}.svc.cluster.local:6379`


## Configuration

See values.yaml for default values