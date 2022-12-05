# metabase-helm-chart

Helm chart for [Metabase Open Source Edition](https://www.metabase.com/start/oss/).

## Prerequisites

Only tested on Kubernetes 1.21+ and Helm 3.

## Installing

```
helm repo add metabase https://hellobaton.github.io/metabase-helm-chart
```

Note: This chart configures Metabase to use an H2 (embedded file) database. This is fine for testing, but for production purposes it is recommended to use a production-ready database that handles backups. For more information see https://www.metabase.com/docs/latest/installation-and-operation/migrating-from-h2

## Values

|              Key              | Type          | Default                    | Description                                                                                       |
|:-----------------------------:|---------------|----------------------------|---------------------------------------------------------------------------------------------------|
| image.repository              | str           | metabase                   | Repository to pull the Docker image from                                                          |
| image.name                    | str           | metabase                   | Name of the Docker image                                                                          |
| image.tag                     | str           | latest                     | Tag of the Docker image to use                                                                    |
| metabase.javaTimezone         | str           | America/New_York           | It's best to set your Java timezone to match the timezone you'd like all your reports to come in. |
| metabase.dbFile               | str           | /metabase-data/metabase.db | The local path to the Metabase application database file                                          |
| metabase.port                 | int           | 80                         | Service port for connecting to Metabase                                                           |
| metabase.memoryLimit          | str           | 2Gi                        | How much memory to grant the pod to use                                                           |
| ingress.enabled               | bool          | false                      | Whether to create an Ingress                                                                      |
| ingress.annotations           | map[str, str] | {}                         | Map to annotate the Ingress with                                                                  |
| ingress.alb.enabled           | bool          | false                      | Whether to create the annotations for an AWS ALB                                                  |
| ingress.alb.subnets           | str           |                            | Comma-separated list of subnets for the ALB                                                       |
| ingress.alb.certificateArn    | str           |                            | ARN for an HTTPS certificate                                                                      |
| persistentVolume.enabled      | bool          | false                      | Whether to create a Persistent Volume for mounting the metabase application database file         |
| persistentVolume.storageClass | str           | gp2                        | The storage class to use for the PVC                                                              |
| persistentVolume.size         | str           | 10Gi                       | The size of the persistent volume                                                                 |