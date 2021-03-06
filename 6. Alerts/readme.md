# Alerts

Alerts allow you to be notified when key events happen in your Kubernetes environment. Calico supports alerting on the following datasets:

* Audit Logs
* DNS Logs
* Flow Logs

> Alerts can be configured either through the CLI or through the Calico Cloud UI.

## Alert Examples

Here are a few common example alerts that can be configured through manifests:

**Detect SSH traffic in the 'hipstershop' namespace:**

```yaml
kubectl apply -f -<<EOF
apiVersion: projectcalico.org/v3
kind: GlobalAlert
metadata:
  name: network.ssh-to-hipstershop
spec:
  description: "ssh flows to hipstershop namespace"
  summary: "[flows] ssh flow in hipstershop namespace detected from ${source_namespace}/${source_name_aggr}"
  severity: 100
  period: 10m
  lookback: 10m
  dataSet: flows
  query: proto='tcp' AND action='allow' AND dest_port='22' AND (source_namespace='hipstershop' OR dest_namespace='hipstershop') AND reporter=src
  aggregateBy: [source_namespace, source_name_aggr]
  field: num_flows
  metric: sum
  condition: gt
  threshold: 0
EOF
```



**Monitor for priviledge access in the cluster and detect any modification to 'globalnetworksets':**

```yaml
kubectl apply -f -<<EOF
apiVersion: projectcalico.org/v3
kind: GlobalAlert
metadata:
  name: policy.globalnetworkset
spec:
  description: "Changed globalnetworkset"
  summary: "[audit] [privileged access] change detected for ${objectRef.resource} ${objectRef.name}"
  severity: 100
  period: 10m
  lookback: 10m
  dataSet: audit
  query: (verb=create OR verb=update OR verb=delete OR verb=patch) AND "objectRef.resource"=globalnetworksets
  aggregateBy: [objectRef.resource, objectRef.name]
  metric: count
  condition: gt
  threshold: 0
EOF
```

### Reference Documentation

[Calico Global Alerts](https://docs.tigera.io/visibility/alerts#create-a-global-alert)
[Calico Global Alert Reference](https://docs.tigera.io/reference/resources/globalalert)


