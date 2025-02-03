# Ansible Role: Loki YARA Scanner

This Ansible role installs and configures Loki YARA IOC Scanner on target systems. It handles the download, installation, execution of scans, and collection of scan reports.

## Requirements

- Ansible 2.9 or higher
- Python 3.x on target systems
- Git installed on target systems

## Role Variables

See `defaults/main.yml` for all available variables.

### Custom YARA Rules

The role supports adding custom YARA rules in two ways:

1. By specifying a directory containing YARA rules:
```yaml
loki_custom_rules_path: "/path/to/your/yara/rules/directory"
```

2. By specifying individual YARA rule files:
```yaml
loki_custom_rules_files:
  - "/path/to/rule1.yar"
  - "/path/to/rule2.yar"
```

Additional YARA configuration:
```yaml
# Whether to delete existing custom rules before copying new ones
loki_delete_existing_custom_rules: false

# Directory where custom rules will be stored on the target
loki_custom_rules_dir: "{{ loki_install_dir }}/Loki/signature-base/custom"
```

## Dependencies

- `farisc0de.epel`

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: ansible-role-loki
      vars:
        loki_report_name: "custom-scan-report"
        loki_custom_rules_path: "/path/to/custom/yara/rules"
        loki_custom_rules_files:
          - "/path/to/specific/rule.yar"
```

## Tags

- `loki_setup`: Setup and installation tasks
- `loki_rules`: Custom YARA rules management
- `loki_update`: Update signatures
- `loki_scan`: Run scan
- `loki_report`: Report collection

## License

MIT

## Author Information

Created in 2025
