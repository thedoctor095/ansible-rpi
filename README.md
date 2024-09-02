# Raspberry Pi Setup with Ansible: Automated Security, Logging, and System Updates
<p align="center">
    <a href="https://opensource.org/licenses/MIT" alt="MIT License">
        <img src="https://img.shields.io/badge/License-MIT-green.svg" /></a>
    <a href="https://ansible.com" alt="Ansible 2.16.9">
        <img src="https://img.shields.io/badge/Ansible-2.16.9-green.svg" /></a>
    <a href="https://www.python.org/downloads/release/python-3100/" alt="Python3.10">
        <img src="https://img.shields.io/badge/Python-3.10-green.svg" /></a>
</p>


The project consists of 6 playbooks designed to automate the setup of a Raspberry Pi running on Raspbian.
## Project Tree Overview
```
.
├── ansible.cfg
├── inventory
│   └── hosts.yml
├── JetBrains.gitignore
├── LICENSE
├── playbooks
│   ├── configure_logging.yml
│   ├── configure_security.yml
│   ├── ping_connection.yml
│   ├── post_install_cleanup.yml
│   ├── run_all.yml
│   └── update_system.yml
├── README.md
└── roles
    ├── check_connection
    │   └── tasks
    │       └── main.yml
    ├── post_install_cleanup
    │   └── tasks
    │       └── main.yml
    ├── setup_logging
    │   ├── files
    │   │   ├── loki_config.yaml
    │   │   └── promtail_config.yaml
    │   └── tasks
    │       └── main.yml
    ├── setup_security
    │   ├── handlers
    │   │   └── main.yml
    │   ├── tasks
    │   │   └── main.yml
    │   └── vars
    │       └── main.yml
    └── setup_system_updating
        ├── tasks
        │   └── main.yml
        └── vars
            └── main.yml
```

## Project Structure

### 1. Connection and compatibility checks
The playbook ensures the Raspberry Pi is reachable by pinging the server and confirms whether the system is running Debian-based OS before going further.


**Playbook Path:** `playbooks/ping_connection.yml`

### 2. System updates and unattended-upgrades
The playbook updates and upgrades system packages, cleans up the APT repository, and installs and configures `unattended-upgrades` for automated security updates.

**Playbook Path:** `playbooks/update_system.yml`

### 3. System security
The playbook focuses on securing the Raspberry Pi, configuring SSH and`sudoers`, disables IPv6, and installs and configures UFW firewall and Fail2ban.

**Playbook Path:** `playbooks/configure_security.yml`

### 4. Logging setup
The playbook installs and configures Grafana, Grafana-Loki and Promtail to centralize the system logs.

**Playbook Path:** `playbooks/configure_logging.yml`

### 5. System cleanup
The playbook removes unused packages, performs a repository cleanup and removes unused dependencies. 

**Playbook Path:** `playbooks/post_install_cleanup.yml`

### 6. Run all playbooks
The last playbook runs all the previously mentioned playbooks in order.

**Playbook Path:** `playbooks/run_all.yml`

## Dependencies
- Ansible >= 2.16.9
## How to run all the playbooks
```ansible-playbook playbooks/run_all.yml```

## Example playbook`playbooks/run_all.yml`
```yaml
---

- import_playbook: ping_connection.yml
- import_playbook: update_system.yml
- import_playbook: configure_security.yml
- import_playbook: configure_logging.yml
- import_playbook: post_install_cleanup.yml
```

## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/thedoctor095/ansible-rpi/blob/master/LICENSE) file for details.

## Contributors
Feel free to contribute to the project by forking the repository, make your changes and open a pull request from your fork's branch to the original repository master branch.

## Reporting Issues
If you find a bug or have a feature request, please open an issue and provide as much detail as possible.
