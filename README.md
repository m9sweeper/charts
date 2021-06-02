# Minesweeper Helm Chart
## Install
To claim a free license go to [m9sweeper licensing](licensing.m9sweeper.io)

## Configuration

If postgresql is enabled, then it will deploy postgres db. Set to false to use an external postgres DB
```yaml
postgres:
  enabled: true
```

If rabbitmq is enabled, then it will deploy rabbitmq. Set to false to use an external rabbitmq.
```yaml
rabbitmq:
  enabled: true
```

The following table lists the configurable parameters of the chart and the default values.


| Parameter                                                                   | Description                                                                                                        | Default                         |
| --------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------| ------------------------------- |
| **postgresql properties**                                                   |
|
| `Global.postgres.host`                                                      | postgresql hostname                                                                                                | `minesweeper-postgres`          |
| `Global.postgres.username`                                                  | postgresql username                                                                                                | `postgres`                      |
| `Global.postgres.password`                                                  | postgresql password                                                                                                | `postgres`                      |
| `Global.postgres.database`                                                  | postgresql database                                                                                                | `postgres`                      |
| `Global.postgres.port`                                                      | postgresql port                                                                                                    | `5432`                          |
|
| **rabbitmq properties**
|
| `Global.rabbitmq.host`                                                      | rabbitmq hostname                                                                                                  | `minesweeper-rabbitmq`          |
| `Global.rabbitmq.port`                                                      | rabbitmq port                                                                                                      | `5672`                          |
| `Global.rabbitmq.username`                                                  | rabbitmq username                                                                                                  | `guest`                         |
| `Global.rabbitmq.password`                                                  | rabbitmq password                                                                                                  | `guest`                         |
| `Global.rabbitmq.queueName`                                                 | rabbitmq queue name                                                                                                | `trawler_queue`                 |
| `Global.jwtSecret`                                                          | Provide a secret string that will be used to sign JWT tokens                                                       | `asdfasdfasd`                   |
| `Global.baseUrl`                                                            | URL will be used in email templates to reference a http link to Dash                                               | `localhost:3000`                |
| `Global.apiKey`                                                             | Provide a secret string that will be set as the first Dash user's API key                                          | `1234567890`                    |
|
| **Dash Properties**                                                          |
|
| `dash.image.registry`                                                       | Registry for Dash Helm chart                                                                                       | `dockerhub.io`                  |
| `dash.image.repository`                                                     | Repository for Dash Helm chart                                                                                     | `m9sweeper/dash`                |
| `dash.image.tag`                                                            | Tag for Dash Helm chart                                                                                            | `latest`                        |
|
| **values that will be used to initialize the Dash database during installation**
|
| `dash.init.clusterGroupName`                                                | Dash Init clusterGroupName                                                                                         | `default-cluster-group`         |
| `dash.init.clusterName`                                                     | Dash Init clusterName                                                                                              | `default-cluster`               |
| `dash.init.superAdminEmail`                                                 | Dash Init superAdminEmail                                                                                          | `admin@test.com`                |
| `dash.init.superAdminPassword`                                              | Dash Init superAdminPassword                                                                                       | `superadmin4me`                 |
| `dash.init.licenseKey`                                                      | Dash Init licenseKey for permission to run project                                                                 | ``                   |
| `dash.init.instanceKey`                                                     | Dash Init instanceKey for permission to run project                                                                | ``                   |
| `dash.init.docker.registries.name`                                          | Dash Init Registry Name                                                                                            | ``             |
| `dash.init.docker.registries.hostname`                                      | Dash Init Registry Hostname                                                                                        | ``        |
| `dash.init.docker.registries.login_required`                                | Dash Init login_required                                                                                           | ``                          |
| `dash.init.docker.registries.username`                                      | Dash Init Registry Username                                                                                        | ``                           |
| `dash.init.docker.registries.password`                                      | Dash Init password                                                                                                 | ``                        |
| **Trawler Configuration**                                                   |
| `trawler.image.registry`                                                    | Registry for Trawler Helm chart                                                                                    | `dockerhub.io`                  |
| `trawler.image.repository`                                                  | Repository for Trawler Helm chart                                                                                  | `m9sweeper/trawler`             |
| `trawler.image.tag`                                                         | Tag for Trawler Helm chart                                                                                         | `latest`                        |
|
| **Dash Email Properties**                                                   |
|
| `dash.email.method`                                                         | Email method options are SMTP or SENDGRID                                                                          | `SMTP`                            |
| `dash.email.smtp.host`                                                      | Choose smtp host                                                                                                   | `localhost`                     |
| `dash.email.smtp.port`                                                      | Choose smtp port                                                                                                   | `465`                           |
| `dash.email.smtp.tlsRequired`                                               | Choose smtp tls authentication required or not                                                                     | `true`                    |
| `dash.email.smtp.user`                                                      | Choose smtp username                                                                                               | `smtp`                          |
| `dash.email.smtp.password`                                                  | Choose smtp password                                                                                               | `smtp`                          |
| `dash.email.sendgridApiKey`                                                 | Choose email sendgridApiKey                                                                                        | ''                       |
| `dash.email.senderEmail`                                                    | Choose email senderEmail                                                                                           | ``           |
| `dash.email.enableSystemErrorEmail`                                         | Enable/disable system error email notifications                                                                    | `false`                 |
| `dash.email.systemErrorMailTo`                                              | The email address to send system error emails to                                                                   | ``           |
|
| **Dash Ingress Properties**                                                 |
|
| `dash.ingress.hosts`                                                        | Add lists of hosts                                                                                                | ``                  |
| `dash.ingress.path`                                                         | Add backend endpoint path                                                                                         | `/`                              |
| `dash.ingress.k8sIngress.enabled`                                           | Set true to enable nginx ingress                                                                                  | `false`                  |
| `dash.ingress.k8sIngress.annotations`                                       | Add annotations for nginx ingress                                                                                 | `kubernetes.io/ingress.class: nginx`                          |
| `dash.ingress.k8sIngress.tls.secretName`                                    | K8s secret where certificate is stored                                                                | `tls-secret`                     |
| `dash.ingress.k8sIngress.tls.hosts`                                         | Write hostname for apply tls                                                                                      | ``                  |
| **Istio Config - VirtualService, DestinationRule, Gateway (optional), PeerAuthentication (optional)**
| `dash.ingress.istio.enabled`                                                | Set true to enable Istio or false to disable                                                                      | `false`                  |
| `dash.ingress.istio.gateways.create`                                        | Set true to enable create istio gateways                                                                          | `false`                  |
| `dash.ingress.istio.gateways.gatewayRefs`                                   | Provide name to create istio gateway                                                                              | `istio-system/example`           |
| `dash.ingress.istio.loadBalancerType`                                       | Write name of loadBalancerType                                                                                    | `ROUND_ROBIN`                    |
| `dash.ingress.istio.mtlsMode`                                               | Set mtls mode, options are: PERMISSIVE or STRICT                                                                  | `PERMISSIVE`                     |






