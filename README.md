# security

Role that manages security settings. For now:

- manages sshd params
- ensures /root has strict permissions
- hardens permissions for grub.cfg and a bunch of other dirs/files, see `security_permissions` list in [defaults](defaults/main.yml)
- manages hidepid param for /proc
- disables auto-upgrades

## Deploy example (do not copy blindly!)

```yaml
    - role: security
      security_disable_hidepid_changing: true
```

## Available parameters

| Param | Description |
| -------- | -------- |
| `default_sshd_params` | contains list of default params for sshd, doublecheck if you override it! |
| `default_sysctl_params` | contains list of default system params, doublecheck if you override it! |
| `sshd_params` | list for setting custom params for sshd, empty by default |
| `security_disable_hidepid_changing` | if set to "true" - hidepid setup will be skipped. This will not revert any of already made mount options or scripts |
| `security_permissions` | see [defaults](defaults/main.yml) | list, describing proper permissions for dirs/files, that will be set |

## FAQ

### Is there a way to skip some configuration entirely

You can skip only hidepid setup so far. Or you can override default lists of sshd params with empty ones.

## TODO

- add skip option. for example: skip ssh configuration
- improve detection of installed unattended-upgrades after [this issue](https://github.com/ansible/ansible/issues/60889)
- improve tests (and clean out commented garbage)
