# helm-charts

## 参数说明

| 参数                              | 描述                                       |
| ------------------------------- | ---------------------------------------- |
| `prefix`                        | 前缀，组合结果为`prefix`+`*`+`suffix`，`*`必须有     |
| `suffix`                        | 后缀，组合结果为`prefix`+`*`+`suffix`，`*`必须有     |
| `*`                             | 除`perfix`和`suffix`外，第一级开头的代表一个服务，可任意命名，一个`values.yaml`中至少包含一项`*` |
| `*.image`                       | image仓库                                  |
| `*.tag`                         | image版本号                                 |
| `*.pullSecret`                  | image拉取`secret`名                         |
| `*.restartPolicy`               | 重启策略，可选项`Always`，` OnFailure`，`Never`，默认`Always`，更多参考官网解释 |
| `*.command`                     | 参考官网解释                                   |
| `*.args`                        | 参考官网解释                                   |
| `*.count`                       | 要部署的服务个数，默认为1                            |
| `*.annotations`                 | `deployment`的`annotations`               |
| `*.port`                        | 数组格式，每一项可有一个或两个值，中间用`:`分割，左边代表`service`端口，右边代表容器端口，如果同时左右同时存在则会创建`service`，例`80:8080`或`80` |
| `*.host`                        | 对象格式，`key`为`port`中左边暴露的`service`端口，`value`为对应的域名，一个端口多个域名用`;`隔开，例`80: api.example.com`或`80: api2.example.com `，填写的域名需要解析到`kubernetes`节点`IP`，如果整个`values.yaml`中没有一个`.host`将不会创建`ingress.yaml`，如果有每一个对象将创建一个`ingress.yaml` |
| `*.tls`                         | 对象格式，`key`为`secretName`，`value`为`*.host`中的域名，默认不启用证书 |
| `*.serviceAnnotations`          | `service`的`annotations`                  |
| `*.ingressAnnotations`          | `ingress`的`annotations`                  |
| `*.env`                         | 对象格式，`key`为环境环境变量名，`value`为环境变量值         |
| `*.livenessProbe`               | 参考官网解释                                   |
| `*.readinessProbe`              | 参考官网解释                                   |
| `*.resources`                   | 参考官网解释                                   |
| `*.initContainers`              | 参考官网解释                                   |
| `*.secret`                      | 创建一个`secret`                             |
| `*.configMap`                   | 创建一个`configMap`                          |
| `*.volumes`                     | 生成挂载目录                                   |
| `*.volumes.[*]`                 | 可用选项`hostPath`,`nfs`,`configMap`,`secret`声明使用什么类型的卷 |
| `*.volumes.hostPath.type`       | `hostPath`类型                             |
| `*.volumes.hostPath.path`       | 数组格式，每项格式为`挂载目录:容器目录:子路径:是否只读`，例`/data/:/var/html:a.yaml:true`，其中子路径和是否只读可省略 |
| `*.volumes.nfs.server`          | `nfs`服务器地址                               |
| `*.volumes.nfs.path`            | 参考`*.volumes.hostPath.path`              |
| `*.volumes.configMap.[*]`       | `configMap`的名字                           |
| `*.volumes.configMap.[*].path`  | 数组格式，每项格式为`容器目录:子路径:是否只读`，例`/var/html:a.yaml:true`，其中子路径和是否只读可省略 |
| `*.volumes.configMap.[*].items` | 数组格式，每项格式为`单独挂载的Key:子路径`，例`a.yaml:sub`   |
| `*.volumes.secret.[*]`          | `secret`的名字                              |
| `*.volumes.secret.[*].path`     | 参考`*.volumes.configMap.[*].path`         |
| `*.volumes.secret.[*].items`    | 参考`*.volumes.configMap.[*].items`        |

