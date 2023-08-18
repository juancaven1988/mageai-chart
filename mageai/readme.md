# MageAI Helm Chart

## Description

This Helm Chart deploys MageAI, a powerful data processing tool, onto a Kubernetes cluster. It provides configurable options for deploying various components of MageAI.

## Resources Created

This Helm Chart deploys the following Kubernetes resources:

### ConfigMap

- ConfigMap for MageAI configuration settings.

### Deployment

- Main deployment for the MageAI application.
- Scheduler deployment for the MageAI scheduler component.

### Service

- Service for exposing the MageAI application.

### Ingress

- Ingress for accessing the MageAI application via a web browser.

### PersistentVolumeClaim

- PersistentVolumeClaim for persisting data used by MageAI.

## Configuration Values

Below is a table detailing the configurable values that can be set in the `values.yaml` file:



| Name                                   | Description                                | Default                  |
|----------------------------------------|--------------------------------------------|--------------------------|
| `image.repository`                     | Docker image repository for MageAI.        | `mageai/mageai`          |
| `image.pullPolicy`                     | Image pull policy.                         | `IfNotPresent`           |
| `image.tag`                            | Image tag for MageAI.                      | `"latest"`               |
| `team`                                 | The team responsible for MageAI.           | `"team"`                 |
| `imagePullSecrets`                     | List of image pull secrets.                | `[]`                     |
| `nameOverride`                         | Override the name of the chart.            | `"mage"`                 |
| `fullnameOverride`                     | Override the full name of the chart.       | `"mage-ai"`              |
| `proyectFolder`                        | The project folder for MageAI.             | `"/home/src/proyect_name"` |

| `podAnnotations`                       | Annotations for the pods.                  | `{}`                     |
| `podSecurityContext`                   | Security context for pods.                | `{}`                     |
| `securityContext`                      | Security context for containers.          | `{}`                     |
| `nodeSelector` | Node labels for the pods | `{}` |
| `tolerations` | Tolerations labels for the pods | `[]` |
| `affinity` | Affinity labels for the pods | `{}` |
| `env` | Enviroment variables for the pods | `[]` |
#### Service Account

| Name                                   | Description                                | Default                  |
|----------------------------------------|--------------------------------------------|--------------------------|
| `serviceAccount.create`                | Create a service account.                  | `false`                  |
| `serviceAccount.annotations`           | Annotations for the service account.       | `{}`                     |
| `serviceAccount.name`                  | Name of the service account to use.        | `"mage"`                 |
#### Role

| Name                                   | Description                                | Default                  |
|----------------------------------------|--------------------------------------------|--------------------------|
| `role.create`                          | Create a kube role for MageAI.                  | `true`                   |
| `role.name`                            | Name of the role for MageAI.               | `"job-manager"`          |
| `role.namebind`                        | Name to bind the role to.                  | `"job-manager"`          |


### Scheduler Configuration
| Name                                   | Description                                | Default                  |
|----------------------------------------|--------------------------------------------|--------------------------|
| `scheduler.enable`                     | Enable the scheduler component.            | `false`                  |
| `scheduler.resources.limits.cpu`        | CPU limit for the scheduler.               | `2`                      |
| `scheduler.resources.limits.memory`     | Memory limit for the scheduler.            | `4G`                     |
| `scheduler.resources.requests.cpu`      | CPU request for the scheduler.             | `40m`                    |
| `scheduler.resources.requests.memory`   | Memory request for the scheduler.          | `350Mi`                  |
| `scheduler.redis.url`                  | URL for the Redis instance.                | `"host:port"`            |
| `scheduler.autoscaling.enabled`         | Enable autoscaling for the scheduler.      | `true`                   |
| `scheduler.autoscaling.minReplicas`     | Minimum number of scheduler replicas.      | `1`                      |
| `scheduler.autoscaling.maxReplicas`     | Maximum number of scheduler replicas.      | `3`                      |
| `scheduler.autoscaling.targetCPUUtilizationPercentage`     | CPU trget for HPA.      | `1000`                      |
| `scheduler.autoscaling.targetMemoryUtilizationPercentage`     | Memory target for HPA      | `1000`                      |
### Web Server Configuration

| Name                                   | Description                                | Default                  |
|----------------------------------------|--------------------------------------------|--------------------------| 
| `web.resources.limits.cpu`              | CPU limit for the web component.           | `2`                      |
| `web.resources.limits.memory`           | Memory limit for the web component.        | `4G`                     |
| `web.resources.requests.cpu`              | CPU required for the web component.           | `40m`                      |
| `web.resources.requests.memory`           | Memory required for the web component.        | `350Mi`                     |
| `web.autoscaling.enabled`         | Enable autoscaling for the web component.      | `true`                   |
| `web.autoscaling.minReplicas`     | Minimum number of scheduler replicas.      | `1`                      |
| `web.autoscaling.maxReplicas`     | Maximum number of scheduler replicas.      | `3`                      |
| `web.autoscaling.targetCPUUtilizationPercentage`     | CPU trget for HPA.      | `1000`                      |
| `web.autoscaling.targetMemoryUtilizationPercentage`     | Memory target for HPA      | `1000`                      |
| `web.service.type` | Type of the service for the web component  | ` ` |
| `web.service.port` | Port of the service | `6789` |
| `web.ingress.enable` | Wichever to create or not an Ingress | `false` |
| `web.ingress.className` | Ingress class | ` ` |
| `web.ingress.annotations` | Anotations for the ingress | `{} ` |
| `web.ingress.hosts` | List of host for the Ingress | `[]` |



### PVC Configuration

| Name                                   | Description                                | Default                  |
|----------------------------------------|--------------------------------------------|--------------------------| 
| `persistentVolumeClaim.enable`          | Enable persistent volume claim.            | `true`                   |
| `persistentVolumeClaim.claimName`       | Name of the PVC for MageAI.                | `"mage-pvc"`             |
| `persistentVolumeClaim.storage`         | Storage size for the PVC.                  | `"5Gi"`                  |
| `persistentVolumeClaim.class`           | Storage class for the PVC.                 | `"efs"`                  |
| `persistentVolumeClaim.accessMode`      | Access modes for the PVC.                  | `[]`                     |
### ConfigMap Configuration

| Name                                   | Description                                | Default                  |
|----------------------------------------|--------------------------------------------|--------------------------| 
| `configMap.enable`                      | Enable ConfigMap creation.                 | `true`                   |
| `configMap.name`                        | Name of the ConfigMap for MageAI.          | `"mage-config"`                     |
| `configMap.retention_period`            | Retention Period for the variables.        | `'2d'`                   |
| `configMap.notifications.enable`            | Enable notifications.        | `'false'`                   |
| `configMap.notifications.teams_webhook`            | Webhook for teams notifications.        | `''`                   |
| `configMap.notifications.slack_webhook`            | Webhook for slack notifications.        | `''`                   |
| `configMap.notifications.smtp.host`            | SMTP host for email notifications.        | `''`                   |
| `configMap.notifications.smtp.origin`            | SMTP origin for email  notifications.        | `''`                   |
| `configMap.notifications.smtp.user`            | SMTP user for email notifications.        | `''`                   |
| `configMap.notifications.smtp.password`            | SMTP password for email notifications.        | `''`                   |
| `configMap.notifications.smtp.destinations`            | List of destinations for email notifications.        | `[]`                   |
| `configMap.notifications.alert_on`            | List of alerts triggers.        | `[]`                   |
| `configMap.notifications.message_templates.failure.detail`            | Template for alert message on pipeline failure        | `''`                   |
| `configMap.notifications.message_templates.success.detail`            | Template for alert message on pipeline success       | `''`                   |
| `configMap.notifications.message_templates.sla.detail`            | Template for alert message on pipeline pass sla        | `''`                   |

### Executors

| Name                                   | Description                                | Default                  |
|----------------------------------------|--------------------------------------------|--------------------------| 
| `configMap.workers.log.type`            | Log destinations for executors        | `'s3'`  |
| `configMap.workers.log.bucket`            | Bucket for executors log destination        | `'bucket-name'`  |
| `configMap.workers.log.prefix`            | Prefix  for executors log destination        | `'prefix'`  |
| `configMap.workers.log.path`            | Path  for executors log destination  when destination is gcs     | `''`  |
| `configMap.workers.log.level`            | Level of logs stored from the workers     | `'INFO'`  |
| `configMap.workers.log.retention_period`            | Periodo de retencion de logs in pvc     | `'15d'`  |
| `configMap.workers.log.optionals`            | Optional logging_config values    | `[]`  |
| `configMap.workers.k8s_executor_config.resource_limits.cpu`              | CPU limit for the k8s executors.           | `"1000m"`                      |
| `configMap.workers.k8s_executor_config.resource_limits.memory`           | Memory limit for the k8s executors.        | `"2048Mi"`                     |
| `configMap.workers.k8s_executor_config.resource_requests.cpu`              | CPU required for the k8s executors.           | `500m`                      |
| `configMap.workers.k8s_executor_config.resource_requests.memory`           | Memory required for the k8s executors.        | `1024Mi`                     |
| `configMap.workers.k8s_executor_config.prefix`           | The kubernetes job name is in this format: mage-{job_name_prefix}-block-{block_run_id}. | `"data-prep"`                     |
| `configMap.workers.concurrency`           | maximum number of concurrent block runs | `"20"`                     |
| `configMap.retry_config.retries`           | maximum number of retries | `"2"`                     |
| `configMap.retry_config.delay`           | Delay between retries in seconds | `"60"`                     |
| `configMap.retry_config.max_delay`           | Max Delay between retries in seconds | `"180"`                     |
| `configMap.retry_config.exponential`           | If the delay between retrais should be exponential or not | `"true"`                     |
| `configMap.io_config`           | A series of conection credentials for the default profile | `{}`                     |




For a complete list of configurable values, please refer to the `values.yaml` file.

## Usage

To deploy MageAI using this Helm Chart, use the following command:

```sh
helm install mageai ./path/to/mageai-chart