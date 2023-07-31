# wireguard

![Version: 0.14.0](https://img.shields.io/badge/Version-0.14.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.0.0](https://img.shields.io/badge/AppVersion-0.0.0-informational?style=flat-square)

A Helm chart for managing a wireguard vpn in kubernetes

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| bryopsida |  |  |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{"podAntiAffinity":{"requiredDuringSchedulingIgnoredDuringExecution":[{"labelSelector":{"matchLabels":{"app":"{{ .Release.Name }}-wireguard","role":"vpn"}},"topologyKey":"kubernetes.io/hostname"}]}}` | Set pod affinity or antiAffinity |
| autoscaling.enabled | bool | `true` |  |
| autoscaling.maxReplicas | int | `10` |  |
| autoscaling.minReplicas | int | `3` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `75` |  |
| configSecretName | string | `nil` | If provided, this secret will be used instead of the config created from the helm value scope |
| configSecretProperty | string | `"wg0.conf"` | The property/key on the secret holding the wireguard configuration file |
| daemonSet | bool | `false` | Run as a DaemonSet instead of Deployment |
| deploymentStrategy.rollingUpdate.maxSurge | int | `1` |  |
| deploymentStrategy.rollingUpdate.maxUnavailable | int | `0` |  |
| deploymentStrategy.type | string | `"RollingUpdate"` |  |
| disableConfigManagement | bool | `false` | Disable creation and any mount of the wireguard confifugration file, this assumes another mechanism is provided/used to manage a configuration file |
| disablePrivateKeyManagement | bool | `false` | Disable creation and any mounting of a private key, this assumes another mechanism is provided/used at the container level to fetch the private key |
| disruptionBudget.enabled | bool | `true` |  |
| disruptionBudget.minAvailable | int | `2` |  |
| extraEnv | object | `{}` | Provide additional environment variables to the wireguard container |
| image.pullPolicy | string | `"Always"` |  |
| image.repository | string | `"ghcr.io/bryopsida/wireguard"` |  |
| image.tag | string | `"main"` |  |
| keygenJob.command | list | `["/job/entry-point.sh"]` | Specify the script to run to generate the private key |
| keygenJob.containerSecurityContext.allowPrivilegeEscalation | bool | `false` |  |
| keygenJob.containerSecurityContext.privileged | bool | `false` |  |
| keygenJob.containerSecurityContext.readOnlyRootFilesystem | bool | `true` |  |
| keygenJob.containerSecurityContext.runAsGroup | int | `1000` |  |
| keygenJob.containerSecurityContext.runAsNonRoot | bool | `true` |  |
| keygenJob.containerSecurityContext.runAsUser | int | `1000` |  |
| keygenJob.extraEnv | object | `{}` | Add additional environment variables to the key generation job, supports helm templating |
| keygenJob.extraScripts | object | `{}` | Inject additional scripts into the key generation job |
| keygenJob.image.pullPolicy | string | `"Always"` |  |
| keygenJob.image.repository | string | `"ghcr.io/curium-rocks/wg-kubectl"` |  |
| keygenJob.image.tag | string | `"latest"` |  |
| keygenJob.podSecurityContext.fsGroup | int | `1000` |  |
| keygenJob.podSecurityContext.fsGroupChangePolicy | string | `"Always"` |  |
| keygenJob.podSecurityContext.seccompProfile.type | string | `"RuntimeDefault"` |  |
| labels | object | `{}` |  |
| nodeSelector | object | `{}` | Set pod nodeSelector, a simplified version of affinity |
| podAnnotations | object | `{}` |  |
| replicaCount | int | `3` |  |
| resources.limits.cpu | string | `"100m"` |  |
| resources.limits.memory | string | `"256Mi"` |  |
| resources.requests.cpu | string | `"100m"` |  |
| resources.requests.memory | string | `"256Mi"` |  |
| runtimeClassName | string | `nil` | Override the default runtime class of the container, if not provided `runc` will most likely be used |
| secretName | string | `nil` | Name of a secret with a wireguard private key on key privatekey, if not provided on first install a hook generates one. |
| securityContext.allowPrivilegeEscalation | bool | `true` |  |
| securityContext.privileged | bool | `false` |  |
| securityContext.readOnlyRootFilesystem | bool | `true` |  |
| securityContext.runAsNonRoot | bool | `true` |  |
| securityContext.runAsUser | int | `1000` |  |
| service.enabled | bool | `true` | Whether the service will be created or not |
| service.nodePort | int | `31820` | Node port, only valid with service type: NodePort |
| service.port | int | `51820` | Service port, default is 51820 UDP |
| service.type | string | `"LoadBalancer"` | Service type, to keep internal to cluster use ClusterIP or NodePort |
| tolerations | list | `[]` | Set pod tolerations |
| volumeMounts | object | `{}` | Passthrough pod volume mounts |
| volumes | object | `{}` | Passthrough pod volumes |
| wireguard.clients | list | `[]` | A collection of clients that will be added to wg0.conf, accepts objects with keys PublicKey and AllowedIPs, stored in secret |
| wireguard.serverAddress | string | `"10.34.0.1/24"` | Address of the VPN server |
| wireguard.serverCidr | string | `"10.34.0.0/24"` | Subnet for your VPN, take care not to clash with cluster POD cidr |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.11.0](https://github.com/norwoodj/helm-docs/releases/v1.11.0)
