# Monitoring Stack Setup

This README provides instructions for setting up a monitoring stack using Grafana, InfluxDB, and Telegraf in a Kubernetes environment.

## Components

The monitoring stack consists of the following components:

1. **Grafana**: An open-source monitoring and observability platform for visualizing data.
2. **InfluxDB**: A high-performance, distributed, and scalable time-series database.
3. **Telegraf**: An agent used to collect and send metrics and data to InfluxDB.

## Prerequisites

Before you begin, ensure you have the following prerequisites:

- Kubernetes cluster up and running.
- `kubectl` command-line tool configured to access your cluster.
- Kubernetes `secrets` and `configMap` resources with appropriate values for authentication and configuration.

## Deployment

Follow these steps to deploy the monitoring stack:

1. Apply the Kubernetes resources using `kubectl apply`:

   ```bash
   kubectl apply -f grafana-influxdb-telegraf.yaml
Verify that the resources are created:

bash
kubectl get deployments,svc,secret,pvc
Ensure that all resources are in a Running or Active state.

## Access Grafana
To access the Grafana dashboard, follow these steps:

Expose the Grafana service:

bash
kubectl port-forward svc/grafana-service 3000:3000
Open a web browser and go to http://localhost:3000.

Log in using the following credentials:

Username: admin
Password: (base64-decoded value of admin-password from the grafana-secrets secret)
You can now configure Grafana data sources and dashboards.

## Access InfluxDB
InfluxDB is used as a data store by Telegraf. You can access it for debugging or querying purposes:

Port forward the InfluxDB service:

bash
kubectl port-forward svc/influxdb-service 8086:8086
Use an InfluxDB client (e.g., influx) to connect to InfluxDB at http://localhost:8086.

Log in using the following credentials:

Username: telegraf
Password: (base64-decoded value of admin-password from the influxdb-secrets secret)
Telegraf Configuration
Telegraf is configured using a ConfigMap named telegraf-config. You can customize the configuration by editing the telegraf.conf file within the ConfigMap.

## Cleanup
To remove the monitoring stack, use the following command:

bash
kubectl delete -f grafana-influxdb-telegraf.yaml

# Bonus Tip
Import dashboard in Grafana with id - "11777" to monitor health of all endpoints on a single pane of window.

Additional Information
Grafana: https://grafana.com/docs/grafana/latest/getting-started/getting-started-k8s/
InfluxDB: https://docs.influxdata.com/influxdb/v1.8/introduction/install/
Telegraf: https://docs.influxdata.com/telegraf/v1.19/introduction/installation/
Feel free to customize and expand on this setup to meet your specific monitoring and observability requirements.