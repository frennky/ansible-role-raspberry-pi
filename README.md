ansible-role-raspberry-pi
=========================

This role configures Raspberry Pi OS.

Requirements
------------

None.

Role Variables
--------------

All default variables are set in `defaults/main.yml`. To change auto upgrade configuration use following variables:

```yaml
# auto upgrade
pi_auto_upgrade_reboot: "true"
pi_auto_upgrade_reboot_time: "03:00"
pi_auto_upgrade_blacklist: []
```

Boot config template contains only settings for PoE fan speeds, wifi, bt, audio, hdmi and gpu. This template is appended to existing file.

```yaml
# boot config
pi_boot_config_template: "config.txt.j2"
```

Fail2ban configuration uses template and port, you can change those with following variables:

```yaml
# fail2ban
pi_fail2ban_configuration_template: "jail.local.j2"
pi_sshd_port: 22
```

Raspberry Pi host name can be set with `pi_hostname` variable, you can override this with `host_vars` in case there's more then one.

```yaml
# hostname
pi_hostname: "raspberry"
```

System upgrade and package installation is controlled with following two variables:

```yaml
# install
pi_upgrade_system: true
pi_packages: []
```

Localization configuration is set with these three variables:

```yaml
# localization
pi_locale: "en_US.UTF-8"
pi_timezone: "Europe/Belgrade"
pi_keyboard_layout: "us"
```

To configure sshd, use following variables:

```yaml
# sshd
pi_sshd_allowtcpforwarding: "yes"
pi_sshd_allowusers:
  - pi
pi_sshd_challengeresponseauthentication: "no"
pi_sshd_maxsessions: 2
pi_sshd_passwordauthentication: "no"
pi_sshd_permitemptypasswords: "no"
pi_sshd_permitrootlogin: "no"
pi_sshd_permittunnel: "no"
pi_sshd_pubkeyauthentication: "yes"
pi_sshd_x11forwarding: "no"

pi_sshd_config:
 - {key: AllowTcpForwarding, value: "{{ pi_sshd_allowtcpforwarding }}"}
 - {key: AllowUsers, value: "{{ pi_sshd_allowusers | join(' ') }}"}
 - {key: ChallengeResponseAuthentication, value: "{{ pi_sshd_challengeresponseauthentication }}"}
 - {key: MaxSessions, value: "{{ pi_sshd_maxsessions }}" }
 - {key: PasswordAuthentication, value: "{{ pi_sshd_passwordauthentication }}"}
 - {key: PermitEmptyPasswords, value: "{{ pi_sshd_permitemptypasswords }}"}
 - {key: PermitRootLogin, value: "{{ pi_sshd_permitrootlogin }}"}
 - {key: PermitTunnel, value: "{{ pi_sshd_permittunnel }}"}
 - {key: PubkeyAuthentication, value: "{{ pi_sshd_pubkeyauthentication }}"}
 - {key: X11Forwarding, value: "{{ pi_sshd_x11forwarding }}"}
```

User account variables are set with following:

```yaml
# user accounts
pi_sudoers_passwordless: []
pi_ssh_user: pi
pi_authorized_key: "~/.ssh/id_ed25519.pub"
```

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- hosts: pi
  roles:
    - ansible-role-raspberry-pi
```

License
-------

MIT

Author Information
------------------

Created by [frennky](https://github.com/frennky).
