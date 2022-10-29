[![Actions Status - Master](https://github.com/juju4/ansible-powershell/workflows/AnsibleCI/badge.svg)](https://github.com/juju4/ansible-powershell/actions?query=branch%3Amaster)
[![Actions Status - Devel](https://github.com/juju4/ansible-powershell/workflows/AnsibleCI/badge.svg?branch=devel)](https://github.com/juju4/ansible-powershell/actions?query=branch%3Adevel)

# powershell ansible role

A simple ansible role to setup powershell, its config and logging under linux.

See also
* https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging_non-windows?view=powershell-7.2
* https://petri.com/how-powershell-7-logging-works-in-linux/

## Requirements & Dependencies

### Ansible
It was tested on the following versions:
 * 2.13

### Operating systems

Tested on Ubuntu 20.04 and 22.04.

## Example Playbook

Just include this role in your list.
For example

```
- host: myhost
  roles:
    - juju4.powershell
```

you probably want to review variables

## Variables

```
powershell_config_template: powershell.config.json.j2
powershell_transcription_outputdir: /var/log/powershell/transcription
powershell_executionpolicy: RemoteSigned
powershell_enablescripts: true
powershell_enablemodule_logging: true
powershell_module_names:
  - '*'
  - PSReadline
  - PowerShellGet
powershell_enableprotectedeventlogging: true
powershell_enabletranscripting: true

powershell_syslog_target: /var/log/powershell/powershell.log

powershell_logrotate_period: 'daily'
powershell_logrotate_rotate: 90
powershell_logrotate_compress: true
powershell_logrotate_delaycompress: true
powershell_logrotate_datext: true
powershell_logrotate_datformat: '-%Y%m%d'
```


## Continuous integration

```
$ pip install molecule docker
$ molecule test
$ MOLECULE_DISTRO=ubuntu:20.04 molecule test --destroy=never
```

## Troubleshooting & Known issues

* ExecutionPolicy setting does not work on Linux
```
PS /root> Set-ExecutionPolicy RemoteSigned
Set-ExecutionPolicy: Operation is not supported on this platform.
```
See also: https://github.com/powershell/powershell/issues/7573, https://github.com/PowerShell/PowerShell/issues/1998, https://learn.microsoft.com/en-us/powershell/scripting/whats-new/unix-support?view=powershell-7.2

## License

BSD 2-clause
