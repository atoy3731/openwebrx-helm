# OpenWebRX Helm Chart

This is a Helm chart to deploy OpenWebRX into Kubernetes and dynamically configure SDR Configurations.

## Usage

To install this chart, utilize `helm` and execute the following:

```bash
helm install -n openwebrx --create-namespace oci://ghcr.io/atoy3731/openwebrx:0.1.0
```

## Parameters

### Deployment Parameters

| Name               | Description                                                  | Value |
| ------------------ | ------------------------------------------------------------ | ----- |
| `replicaCount`     | Number of replicas to run.                                   | `1`   |
| `imagePullSecrets` | imagePullSecrets to pull image from a private registry.      | `[]`  |
| `nodeSelector`     | Node selector for deployment. Do not use if leveraging Akri. | `{}`  |
| `tolerations`      | Tolerations to apply to pods.                                | `[]`  |
| `affinity`         | Affinity settings to apply to pods.                          | `{}`  |

### Image Parameters

| Name               | Description            | Value                |
| ------------------ | ---------------------- | -------------------- |
| `image.repository` | Image repository.      | `jketterl/openwebrx` |
| `image.pullPolicy` | Pull policy for image. | `IfNotPresent`       |
| `image.tag`        | Tag for the image.     | `""`                 |

### Service Account Parameters

| Name                         | Description                                                                                              | Value  |
| ---------------------------- | -------------------------------------------------------------------------------------------------------- | ------ |
| `serviceAccount.create`      | Specifies whether a service account should be created.                                                   | `true` |
| `serviceAccount.automount`   | Automatically mount a ServiceAccount's API credentials?                                                  | `true` |
| `serviceAccount.annotations` | Annotations to attach to service account.                                                                | `{}`   |
| `serviceAccount.name`        | Name of service account. If not set and create is true, a name is generated using the fullname template. | `""`   |

### Pod Parameters

| Name             | Description                              | Value |
| ---------------- | ---------------------------------------- | ----- |
| `podAnnotations` | Additional annotations to add to pod(s). | `{}`  |
| `podLabels`      | Additional labels to add to pod(s).      | `{}`  |

### Service Parameters

| Name               | Description                            | Value       |
| ------------------ | -------------------------------------- | ----------- |
| `service.type`     | Type of service to create.             | `ClusterIP` |
| `service.nodePort` | NodePort to use if type is 'NodePort'. | `30072`     |

### Ingress Parameters

| Name                                 | Description                             | Value                    |
| ------------------------------------ | --------------------------------------- | ------------------------ |
| `ingress.enabled`                    | Specifies whether to create an ingress. | `false`                  |
| `ingress.className`                  | Ingress class name.                     | `""`                     |
| `ingress.annotations`                | Annotations to attach to ingress.       | `{}`                     |
| `ingress.hosts[0].host`              | Hostname for ingress.                   | `chart-example.local`    |
| `ingress.hosts[0].paths[0].path`     | Path for hostname.                      | `/`                      |
| `ingress.hosts[0].paths[0].pathType` | Path type for hostname.                 | `ImplementationSpecific` |
| `ingress.tls`                        | TLS configuration for ingress.          | `[]`                     |

### Resource Parameters

| Name        | Description                                                                    | Value |
| ----------- | ------------------------------------------------------------------------------ | ----- |
| `resources` | Resource configurations. NOTE: See 'values.yaml' for an example of Akri usage. | `{}`  |

### Volumes Parameters

| Name           | Description                     | Value |
| -------------- | ------------------------------- | ----- |
| `volumes`      | Additional volumes to add.      | `[]`  |
| `volumeMounts` | additional volumeMounts to add. | `[]`  |

### Volumes Parameters

| Name        | Description                                                                        | Value               |
| ----------- | ---------------------------------------------------------------------------------- | ------------------- |
| `sdrConfig` | SDR Configurations to inject into OpenWebRX. See 'values.yaml' for default string. | `See 'values.yaml'` |
