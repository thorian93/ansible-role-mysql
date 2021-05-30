# Ansible Role: MySQL

This role installs MySQL on RHEL/CentOS, Debian/Ubuntu and Fedora servers.

[![Ansible Role: MySQL](https://img.shields.io/ansible/role/55139?style=flat-square)](https://galaxy.ansible.com/thorian93/mysql)
[![Ansible Role: MySQL](https://img.shields.io/ansible/quality/55139?style=flat-square)](https://galaxy.ansible.com/thorian93/mysql)
[![Ansible Role: MySQL](https://img.shields.io/ansible/role/d/55139?style=flat-square)](https://galaxy.ansible.com/thorian93/mysql)

## Here be Dragons

**This role has ongoing issues with authentication. Currently I can only advise to use another role like the one by [Jeff Geerling](https://galaxy.ansible.com/geerlingguy/mysql). If I find the time I might fix this role, but for now consider it unmaintained.**

## Known issues

When enabling the automatic backup mechanism currently you have to install `automysqlbackup` yourself when you are on a `RedHat` derivate prior to using this role. Otherwise the role will fail. Configuration can be managed though, as long as you have installed `automysqlbackup` with default settings from their install script.

## Requirements

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: foobar
      roles:
        - role: ansible-role-mysql
          become: yes

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    mysql_login_root_remote: 'false'

If set to `false`, the root user will be prevented from logging in remotely.

    mysql_autobackup_enable: 'false'
    mysql_autobackup_destination: /var/lib/automysqlbackup

Configure automatic backups using `automysqlbackup`.

    mysql_root_user: 'root'
    # mysql_root_pw:
    mysql_backup_user: 'backup'
    # mysql_backup_pw:
    mysql_monitoring_user: 'monitoring'
    # mysql_monitoring_pw:

Configure user accounts for `root`, `backup` and `monitoring` with appropriate grants. If either the name is empty or the password variable is not defined at all, the configuration will be skipped for that user. Be aware, that some tasks might not be carried out in case of the `root` user.

## Dependencies

None.

## OS Compatibility

This role ensures that it is not used against unsupported or untested operating systems by checking, if the right distribution name and major version number are present in a dedicated variable named like `<role-name>_stable_os`. You can find the variable in the role's default variable file at `defaults/main.yml`:

    role_stable_os:
      - Debian 10
      - Ubuntu 18
      - CentOS 7
      - Fedora 30

If the combination of distribution and major version number do not match the target system, the role will fail. To allow the role to work add the distribution name and major version name to that variable and you are good to go. But please test the new combination first!

Kudos to [HarryHarcourt](https://github.com/HarryHarcourt) for this idea!

## Example Playbook

    ---
    - name: "Run role."
      hosts: all
      become: yes
      roles:
        - ansible-role-mysql

## Contributing

Please feel free to open issues if you find any bugs, problems or if you see room for improvement. Also feel free to contact me anytime if you want to ask or discuss something.

## Disclaimer

This role is provided AS IS and I can and will not guarantee that the role works as intended, nor can I be accountable for any damage or misconfiguration done by this role. Study the role thoroughly before using it.

## License

MIT

## Author Information

This role was created in 2020 by [Thorian93](http://thorian93.de/).
