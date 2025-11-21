# teg-envoy-gateway-helm

![Version: 1.5.1](https://img.shields.io/badge/Version-1.5.1-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.5.1](https://img.shields.io/badge/AppVersion-1.5.1-informational?style=flat-square)

The Helm chart for Tetrate Enterprise Gateway for Envoy

**Homepage:** <https://tetrate.io/>

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| oci://docker.io/envoyproxy | gateway-helm | v1.5.4 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| certgen | object | `{"job":{"annotations":{},"resources":{},"ttlSecondsAfterFinished":30},"rbac":{"annotations":{},"labels":{}}}` | TEG Certificate Generation Job configuration used to generate TLS Certificates for Redis |
| config.envoyProxy | object | `{"logging":{"level":{"default":"warn"}}}` | Configuration for every Envoy Proxy replica in each Gateway which uses the default 'teg' GatewayClass (which references the EnvoyProxy resource made from these values). This is merged with defaults to product an EnvoyProxy object (https://gateway.envoyproxy.io/latest/api/extension_types/#envoyproxyspec). Values specified here take precedence. |
| config.envoyProxy.logging.level.default | string | `"warn"` | All Envoy log areas to log at level warn Individual areas can be altered with eg `oauth2: debug` |
| deployment | object | - | Tetrate Enterprise Gateway for Envoy control plane components configuration options |
| deployment.tegEnvoyGateway | object | - | Tetrate Enterprise Gateway for Envoy deployment configuration |
| deployment.tegEnvoyGateway.container | object | `{"securityContext":{"allowPrivilegeEscalation":false,"capabilities":{"drop":["ALL"]},"privileged":false,"readOnlyRootFilesystem":true,"runAsGroup":65532,"runAsNonRoot":true,"runAsUser":65532,"seccompProfile":{"type":"RuntimeDefault"}}}` | Tetrate Enterprise Gateway for Envoy con configuration |
| deployment.tegEnvoyGateway.image | object | - | Tetrate Enterprise Gateway for Envoy image configuration |
| deployment.tegEnvoyGateway.image.pullPolicy | string | `"IfNotPresent"` | Tetrate Enterprise Gateway for Envoy image pull policy |
| deployment.tegEnvoyGateway.image.pullSecrets | list | `[]` | Tetrate Enterprise Gateway for Envoy image pull secrets |
| deployment.tegEnvoyGateway.image.repository | string | `"tetrate/teg-envoy-gateway"` | Tetrate Enterprise Gateway for Envoy image repository |
| deployment.tegEnvoyGateway.image.tag | string | `"v1.5.1"` | Tetrate Enterprise Gateway for Envoy image tag |
| deployment.tegEnvoyGateway.pod | object | `{"affinity":{},"nodeSelector":{},"tolerations":[],"topologySpreadConstraints":[]}` | Tetrate Enterprise Gateway for Envoy pod configuration |
| deployment.tegEnvoyGateway.replicas | int | `1` | Tetrate Enterprise Gateway for Envoy replicas in cluster |
| deployment.tegEnvoyGateway.resources | object | `{}` | Tetrate Enterprise Gateway for Envoy deployment resources More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/ |
| gateway-helm | object | `{"config":{"envoyGateway":{"extensionApis":{"enableEnvoyPatchPolicy":true},"provider":{"kubernetes":{"overwrite_control_plane_certs":false,"rateLimitDeployment":{"container":{"env":[{"name":"LOG_FORMAT","value":"json"},{"name":"REDIS_HEALTH_CHECK_ACTIVE_CONNECTION","value":"false"},{"name":"REDIS_TYPE","value":"SINGLE"},{"name":"REDIS_TLS_CACERT","value":"/redis-certs/ca.crt"}]}}}},"rateLimit":{"backend":{"redis":{"tls":{"certificateRef":{"name":"redis-tls"}},"url":"teg-redis.envoy-gateway-system.svc.cluster.local:6379"},"type":"Redis"}}}}}` | Envoy Gateway installation configuration. Detailed configuration documentation can be found here: https://github.com/envoyproxy/gateway/tree/main/charts/gateway-helm Tetrate Enterprise Gateway for Envoy configures underlying Envoy gateway installation configuration. In case there are any conflicts, between TEG configuration and EG configuration provided here, EG configuration is given precedence. |
| gateway-helm.config.envoyGateway.rateLimit.backend.redis.url | string | `"teg-redis.envoy-gateway-system.svc.cluster.local:6379"` | If you change the namespace or name of the Redis Service, change this to match |
| redis | object | - | TEG Redis deployment configuration |
| redis.disabled | bool | `false` | Redis enabled by default |
| redis.image | object |  - | Redis image configuration |
| redis.image.pullPolicy | string | `"IfNotPresent"` | Redis image pull policy in cluster |
| redis.image.pullSecrets | list | `[]` | Redis image pull secrets |
| redis.image.repository | string | `"redis"` | Redis image repository |
| redis.image.tag | string | `"7.4.2"` | Redis image tag |
| redis.password | string | `""` | default user auth password for redis deployment |
| redis.replicas | int | `1` | Redis replicas to deploy |
| redis.resources | object | `{}` | Redis deployment resources More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/ |
| redis.service | object | - | Redis service configuration |
| redis.service.port | int | `6379` | Redis service exposed port |
| redis.service.type | string | `"ClusterIP"` | Redis service type |

