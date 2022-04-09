
# Ansible Role:  `promtail`

Ansible role to setup [promtail](https://grafana.com/docs/loki/latest/clients/promtail/).


[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/bodsch/ansible-promtail/CI)][ci]
[![GitHub issues](https://img.shields.io/github/issues/bodsch/ansible-promtail)][issues]
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/bodsch/ansible-promtail)][releases]

[ci]: https://github.com/bodsch/ansible-promtail/actions
[issues]: https://github.com/bodsch/ansible-promtail/issues?q=is%3Aopen+is%3Aissue
[releases]: https://github.com/bodsch/ansible-promtail/releases


## Requirements & Dependencies

- None

### Operating systems

Tested on

* Arch Linux
* Debian based
    - Debian 10 / 11
    - Ubuntu 20.10
* RedHat based
    - Alma Linux 8
    - Rocky Linux 8
    - Oracle Linux 8

## usage

### default configuration

```yaml
promtail_version: "2.4.1"
promtail_release_download_url: https://github.com/grafana/loki/releases

promtail_system_user: promtail
promtail_system_group: promtail
promtail_config_dir: /etc/promtail
promtail_storage_dir: /var/lib/promtail

promtail_server: {}

promtail_clients: []

promtail_positions: {}

promtail_scrape_configs: []

promtail_targets: {}
```

### `promtail_server`

[promtail dokumentation](https://grafana.com/docs/loki/latest/clients/promtail/configuration/#server)

```yaml
promtail_server:
  http_listen_address: "127.0.0.1"
  http_listen_port: 9080
  log_level: debug
```

### `promtail_clients`

[promtail dokumentation](https://grafana.com/docs/loki/latest/clients/promtail/configuration/#clients)

```yaml
promtail_clients:
  - url: "http://loki.monitoring.tld"
  - url: "http://127.0.0.1:3100/loki/api/v1/push"
```

### `promtail_positions`

[promtail dokumentation](https://grafana.com/docs/loki/latest/clients/promtail/configuration/#positions)

```yaml
promtail_positions: {}
```

### `promtail_scrape_configs:`

[promtail dokumentation](https://grafana.com/docs/loki/latest/clients/promtail/configuration/#scrape_configs)

```yaml
promtail_scrape_configs:
  # file_sd
  - job_name: file_sd
    file_sd_configs:
      - files:
        - "{{ promtail_config_dir }}//file_sd/*.yml"
        - "{{ promtail_config_dir }}//file_sd/*.yaml"
        - "{{ promtail_config_dir }}//file_sd/*.json"
  #
  - job_name: system
    static_configs:
      - targets:
          - localhost
        labels:
          job: varlogs
          host: "{{ ansible_fqdn }}"
          agent: promtail
          __path__: /var/log/*.log
  # example syslog config
  - job_name: syslog
    syslog:
      listen_address: 0.0.0.0:1514
      labels:
        job: "syslog"
    relabel_configs:
      - source_labels:
          - __syslog_message_hostname
        target_label: 'host'

  - job_name: nginx_access
    static_configs:
      - targets:
          - localhost
        labels:
          job: nginx
          host: "{{ ansible_fqdn }}"
          log_level: access
          agent: promtail
          __path__: /var/log/nginx/*access.log
    pipeline_stages:
      # anonymisier latest octet
      - replace:
          expression: '(?:[0-9]{1,3}\.){3}([0-9]{1,3})'
          replace: '***'
```

For a more comprehensive example, please check out the [molecule](molecule/defaults/group_vars/all/vars.yml) tests!

### `promtail_targets`

[promtail dokumentation](https://grafana.com/docs/loki/latest/clients/promtail/configuration/#target_config)

```yaml
promtail_targets: {}
```


## Contribution

Please read [Contribution](CONTRIBUTING.md)

## Development,  Branches (Git Tags)

The `master` Branch is my *Working Horse* includes the "latest, hot shit" and can be complete broken!

If you want to use something stable, please use a [Tagged Version](https://gitlab.com/bodsch/ansible-promtail/-/tags)!

---

## Author and License

- Bodo Schulz

## License

[Apache](LICENSE)

**FREE SOFTWARE, HELL YEAH!**
