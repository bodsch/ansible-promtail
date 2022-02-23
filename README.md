
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

* Debian based
    - Debian 10 / 11
    - Ubuntu 20.10
* RedHat based
    - CentOS 8 (**not longer supported**)
    - Alma Linux 8
    - Rocky Linux 8
    - Oracle Linux 8
* Arch Linux

## usage

### default configuration

```yaml
promtail_version: "2.4.1"
promtail_release_download_url: https://github.com/grafana/loki/releases

promtail_system_user: promtail
promtail_system_group: promtail
promtail_config_dir: /etc/promtail
promtail_storage_dir: /var/lib/promtail

# https://grafana.com/docs/loki/latest/clients/promtail/configuration/#server
promtail_server: {}

# https://grafana.com/docs/loki/latest/clients/promtail/configuration/#server
promtail_clients: []

# https://grafana.com/docs/loki/latest/clients/promtail/configuration/#positions
promtail_positions: {}

# https://grafana.com/docs/loki/latest/clients/promtail/configuration/#scrape_configs
promtail_scrape_configs: []

# https://grafana.com/docs/loki/latest/clients/promtail/configuration/#target_config
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
