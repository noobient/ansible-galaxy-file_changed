# noobient.file_changed

## Synopsys

This role lets you detect changes in files between operations, so that you can indicate changes if, and only if, the file actually changed.
This is useful when you do ad-hoc commands (`command`, `shell`, etc.) that cannot indicate if changes have been made or not.

## Parameters

| Name | Required | Example | Description |
|---|---|---|---|
| `path` | yes | `/etc/acme/foobar.com/foobar.com.cer` | File to check changes on. |
| `mode` | yes | `before` | Indicate whether the check is before or after the command(s). Possible values are `before` and `after`. If `before`, it calculates the checksum, if `after`, it checks the current checksum with the one calculated during the `before` run, and indicates the change if they differ. |
| `verbose` | no | `true` | If `true`, print more diagnostic messages. Defaults to `false`. |

## Examples

```yml
- include_role:
    name: noobient.file_changed
  vars:
    path: /etc/acme/foobar.com/foobar.com.cer
    mode: before

- name: Do stuff on file
  command:
    cmd: /opt/acme.sh --install-cert -d foobar.com --cert-file /etc/acme/foobar.com/foobar.com.cer
  changed_when: false

- include_role:
    name: noobient.file_changed
  vars:
    path: /etc/foo.conf
    mode: after
    verbose: true
```

## Return Values

| Key | Type | Example | Description |
|---|---|---|---|
| `file_changed.changed` | boolean | `true` | Indicates whether the file changed between the `before` and `after` runs. In `before` mode, it's always `false`. |

## Support

| Platform | Support | Status |
|---|---|---|
| Linter | ✅ | [![Lint](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/lint.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/lint.yml) |
| AlmaLinux 8 | ✅ | [![AlmaLinux 8](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/almalinux-8.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/almalinux-8.yml) |
| AlmaLinux 9 | ✅ | [![AlmaLinux 9](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/almalinux-9.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/almalinux-9.yml) |
| Fedora 37 | ✅ | [![Fedora 37](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/fedora-37.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/fedora-37.yml) |
| Ubuntu 18.04 | ✅ | [![Ubuntu 18.04](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/ubuntu-18.04.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/ubuntu-18.04.yml) |
| Ubuntu 20.04 | ✅ | [![Ubuntu 20.04](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/ubuntu-20.04.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/ubuntu-20.04.yml) |
| Ubuntu 22.04 | ✅ | [![Ubuntu 22.04](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/ubuntu-22.04.yml/badge.svg)](https://github.com/noobient/ansible-galaxy-file_changed/actions/workflows/ubuntu-22.04.yml) |
