# Helm Generic Chart

A Helm chart for deploying the most applications kind by configure some simple values.

## Installation

Before installing this Helm chart, you will need the following:

- A running Kubernetes cluster
- Helm installed on your machine

To install the chart, follow these steps:

1. Add the chart repository to Helm: `helm repo add generic-chart https://shmuel-develeap.github.io/charts-repo/`
2. Update your local Helm chart repository: `helm repo update`
3. Install the chart: `helm install my-release generic -var-file=./my-app-config.yaml`

## Parameters

### Chart parameters

| Name               | Description                                            | Value        |
| ------------------ | ------------------------------------------------------ | ------------ |
| `appKind`          | Application kind: Deployment, StatefulSet or DeamonSet | `Deployment` |
| `nameOverride`     | String to partially override the release name          | `""`         |
| `fullnameOverride` | String to fully override the fullname in templates     | `""`         |

### Application (Deployment/StatefulSet/DaemonSet) parameters

| Name                               | Description                                                                        | Value                                                  |
| ---------------------------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------ |
| `podAnnotations`                   | Chart Pod annotations                                                              | `{}`                                                   |
| `replicaCount`                     | Number of replicas, ignored in DaemonSet                                           | `2`                                                    |
| `image.repository`                 | Image repository                                                                   | `123456789012.dkr.ecr.eu-west-2.amazonaws.com/example` |
| `image.tag`                        | Chart image tag whose default is the chart appVersion                              | `latest`                                               |
| `image.pullPolicy`                 | Chart image pull policy                                                            | `IfNotPresent`                                         |
| `imagePullSecrets`                 | Global Docker registry secret names as an array                                    | `[]`                                                   |
| `ports`                            | Exposed container ports as an array                                                |                                                        |
| `spreadConstraintsByNodes.enabled` | Enable spreading pods on a nodes by max 1 skew                                     | `true`                                                 |
| `environmentVariables`             | Map of key-value pairs that insert in config map                                   | `{}`                                                   |
| `additionalEnvFrom`                | List of secrets and/or config maps for mapping the values as environment variables | `[]`                                                   |
| `additionalEnvValues`              | list of key-value/valueFrom pairs to use as environment variables                  | `[]`                                                   |
| `podSecurityContext`               | pod(s)' Security Context                                                           | `{}`                                                   |
| `containerSecurityContext`         | pod(s)' Security Context                                                           | `{}`                                                   |
| `volumes`                          | Volumes as an array                                                                | `[]`                                                   |
| `volumeMounts`                     | Volume Mounts as an array                                                          | `[]`                                                   |
| `initContainers`                   | Init containers as an array                                                        | `[]`                                                   |
| `resources.limits`                 | Limit definition as max resources that pod will use                                | `{}`                                                   |
| `resources.requests`               | Request definition as resources that pod need to run                               | `{}`                                                   |

### Horizontal Pod Autoscale parameters

| Name                                            | Description                                                             | Value   |
| ----------------------------------------------- | ----------------------------------------------------------------------- | ------- |
| `autoscaling.enabled`                           | Enabling auto scale for the deployment based on resources usage monitor | `false` |
| `autoscaling.minReplicas`                       | Minimum replicas to deploy                                              | `1`     |
| `autoscaling.maxReplicas`                       | Maximum replicas to deploy                                              | `10`    |
| `autoscaling.targetCPUUtilizationPercentage`    | CPU usage percentage for scale-up triggering                             | `80`    |
| `autoscaling.targetMemoryUtilizationPercentage` | Memory usage percentage for scale-up triggering                          | `80`    |

### Service Account parameters

| Name                         | Description                                                                                                            | Value   |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ------- |
| `serviceAccount.create`      | Specifies whether a service account should be created                                                                  | `false` |
| `serviceAccount.annotations` | Annotations to add to the service account                                                                              | `{}`    |
| `serviceAccount.name`        | The name of the service account to use. If not set and create is true, a name is generated using the fullname template | `""`    |

### Service parameters

| Name                   | Description                                       | Value       |
| ---------------------- | ------------------------------------------------- | ----------- |
| `service.enabled`      | Create service for expose deployment as a service | `true`      |
| `service.nameOverride` | service name                                      | `nnn`       |
| `service.port`         | Kubernetes Service port                           | `80`        |
| `service.type`         | Kubernetes Service type                           | `ClusterIP` |
| `service.portName`     | service port name                                 | `""`        |

### Ingress parameters

| Name                  | Description                                                               | Value   |
| --------------------- | ------------------------------------------------------------------------- | ------- |
| `ingress.enabled`     | Create ingress for expose service through load balancer controler service | `false` |
| `ingress.annotations` | Ingress anonotations                                                      | `{}`    |
| `ingress.hosts`       | Ingress host and path parameters                                          | `[]`    |
| `ingress.tls`         | Ingress tls paramters for https protocol ingress                          | `[]`    |
| `nodeSelector`        | Chart Node labels for pod assignment                                      | `{}`    |
| `tolerations`         | Chart Tolerations for pod assignment                                      | `[]`    |
| `affinity`            | Chart Affinity for pod assignment                                         | `{}`    |

## Upgrading

To upgrade the chart, follow these steps:

1. Update your local Helm chart repository: `helm repo update`
2. Upgrade the chart: `helm upgrade my-release generic`

## Troubleshooting

If you encounter any issues when deploying or using this Helm chart, please refer to the following resources:

- Official Kubernetes documentation: https://kubernetes.io/docs/
- Helm documentation: https://helm.sh/docs/
- Support forums for the application you are deploying
```
