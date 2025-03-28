# 内置模块

EMQX 将主题重写、代理订阅等功能通过内置模块的形式提供，支持用户随时启停模块来启停相应功能。目前内置模块已支持以下功能：

| Module Name              | Feature                                |
| ------------------------ | -------------------------------------- |
| `emqx_mod_delayed`       | [延迟发布](../mqtt/mqtt-delayed-publish.md)         |
| `emqx_mod_topic_metrics` | [主题指标统计](../observability/topic-metrics.md) |
| `emqx_mod_subscription`  | [代理订阅](../mqtt/mqtt-auto-subscription.md)    |
| `emqx_mod_acl_internal`  | [内置 ACL](../access-control/authz/authz.md)                |
| `emqx_mod_rewrite`       | [主题重写](../mqtt/mqtt-topic-rewrite.md)         |
| `emqx_mod_presence`      | 上下线通知                             |

EMQX 为内置模块提供了[命令行接口](../admin/cli.md#endpoint-modules)和 [HTTP API](./http-api.md#endpoint-modules)，用户可以很轻松地通过这些接口来启停模块，例如：

```bash
$ ./emqx_ctl modules load emqx_mod_delayed
Module emqx_mod_delayed loaded successfully.
```

```bash
$ curl -i --basic -u admin:public -X PUT "http://localhost:8081/api/v4/nodes/emqx@127.0.0.1/modules/emqx_mod_delayed/load"

{"code":0}
```

当然，用户也可以在 Dashboard 上完成这些操作，包括查看模块状态，这也更加常用。

EMQX 在默认情况下会启动 `emqx_mod_acl_internal` 和 `emqx_mod_presence` 这两个模块，即内置 ACL 与上下线通知功能默认开启。用户可以修改 EMQX `data` 目录下的 `loaded_modules` 文件来更改默认启动的模块。

***默认不启动***

```erlang
{emqx_mod_rewrite, false}.
```

***默认启动***

```erlang
{emqx_mod_rewrite, true}.
```
