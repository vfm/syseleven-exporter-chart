# Project Archive Notice

As of 03.04.2023, this repository has been archived and is no longer actively maintained by vfm. We are pleased to inform you that the project has found a new home and will continue to be developed and maintained by syseleven.

For the latest updates, contributions, issues, and community support, please refer to the new repository at the following URL:

[https://github.com/syseleven/syseleven-exporter](https://github.com/syseleven/syseleven-exporter)

Thank you for your support and understanding.

– vfm-Team

---


# SysEleven Exporter Helm-Chart
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Release Charts](https://github.com/vfm/syseleven-exporter-chart/workflows/Release%20Charts/badge.svg?branch=main)
![Badge](https://img.shields.io/badge/made%20with%20%E2%9D%A4%20by-vfm-002C5B)


A Helm Chart to deploy the greate [SysEleven Exporter](https://github.com/Staffbase/syseleven-exporter) in Kubernetes.

## Usage

Add this Github-Repository as Helm Repository.

```bash
helm repo add syseleven-exporter-repo https://vfm.github.io/syseleven-exporter-chart
helm repo update
```

Now you can install the Chart.

```bash
helm install syseleven-exporter-repo/syseleven-exporter --generate-name
```

Add your Openstack credentials to allow *read-only* access to the API-Endpoint `https://api.cloud.syseleven.net:5001`

```bash
openstack.username
openstack.password
openstack.projectId
```

### Prometheus

If you want an [Prometheus ServiceMonitor](https://github.com/prometheus-operator/prometheus-operator/blob/master/Documentation/api.md#servicemonitor) you can use the `prometheus.serviceMonitor.enabled` flag, which is false by default. The default `serviceMonitor.interval` is 10 minutes, since the API is only polled once per hour by the exporter pod.

```bash
prometheus.serviceMonitor.enabled
prometheus.serviceMonitor.interval 
```

The default Namespace for the ServiceMonitor is the Helm Release Namespace.
If you need the ServiceMonitor in an other namespace, you have to specify the `prometheus.serviceMonitor.namespace`.

```bash
prometheus.serviceMonitor.namespace
```

#### Rules

To use a default set of Prometheus Alertrules, you have to enable the `prometheus.rules.enabled` flag. Simliar to the ServiceMonitor, you can adjust the default Namespace with `prometheus.rules.namespace`.

To see the full list of all options look at [Values.yaml](charts/syseleven-exporter-chart/values.yaml).


#### Dashboard

To use a default Grafana Dashboard, you have to enable the `prometheus.dashboards.enabled` flag. Simliar to the Rules, you can adjust the Namespace with `prometheus.dashboards.namespace`.

To see the full list of all options look at [Values.yaml](charts/syseleven-exporter-chart/values.yaml).
