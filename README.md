# Ansible role `hosts`

An Ansible role for managing the hosts file (`/etc/hosts`). Specifically, the responsibilities of this role are to:

- Add the default localhost entry;
- Add an entry for the host name bound to the host's default external IPv4 address (optional);
- Add entries for basic IPv6 addresses, e.g. ip6-localnet (optional);
- Add entries for Ansible managed hosts (optional);
- Add entries specified in Yaml (optional, see below);
- Add entries specified in text files (optional).

## Requirements

No specific requirements

## Role Variables

None of the variables below are required. When not set, the default setting is applied.

| Variable                                 | Default                              | Comments                                                                                                          |
| :---                                     | :---                                 | :---                                                                                                              |
| `hosts_add_default_ipv4`                 | true                                 | If true, an entry for the host name is added, bound to the host's default IPv4 address.                           |
| `hosts_add_basic_ipv6`                   | false                                | If true, basic IPv6 entries are added (e.g. localhost6, ip6-localnet, etc.)                                       |
| `hosts_add_ansible_managed_hosts`        | false                                | If true, an entry for hosts managed by Ansible is added. (†)                                                      |
| `hosts_add_ansible_managed_hosts_groups` | ['all']                              | Control which host entries are created when using `hosts_add_ansible_managed_hosts` |
| `hosts_entries`                          | []                                   | A list of dicts with custom entries to be added to the hosts file. See below for an example.                      |
| `hosts_file_snippets`                    | []                                   | A list of files containing host file snippets to be added to the hosts file verbatim.                             |
| `hosts_ip_protocol`                      | `ipv4`                               | When adding Ansible managed hosts, this specifies the IP protocol (`ipv4` or `ipv6`)                              |
| `hosts_network_interface`                | `{{ansible_default_ipv4.interface}}` | When adding Ansible managed hosts, this specifies the network interface for which the IP address should be added. |
| `hosts_file_backup`                      | no                                   | If yes, backup of host file is created with timestamp                                                             |
|                                          |                                      |                                                                                                                   |

(†) When setting `hosts_add_ansible_managed_hosts`, an entry for the current host will also be added. Consequently, `hosts_add_default_ipv4` doesn't need to be set.

Individual hosts file entries can be added with `hosts_entries`, a list of dicts with keys `name`, `ip` and (optional) `aliases`. Example:

```Yaml
hosts_entries:
  - name: slashdot
    ip: 216.34.181.45
  - name: gns1
    ip: 8.8.8.8
    aliases:
      - googledns1
      - googlens1
  - name: gns2
    ip: 8.8.4.4
    aliases:
      - googledns2
      - googlens2
```

## Dependencies

No dependencies.

## Example Playbook

See the [test playbook](https://github.com/bertvv/ansible-role-hosts/blob/tests/test.yml)

Tests for this role are provided in the form of a Vagrant environment that is kept in a separate branch, `tests`. I use [git-worktree(1)](https://git-scm.com/docs/git-worktree) to include the test code into the working directory. Instructions for running the tests:

1. Fetch the tests branch: `git fetch origin tests`
2. Create a Git worktree for the test code: `git worktree add tests tests` (remark: this requires at least Git v2.5.0). This will create a directory `tests/`.
3. `cd tests/`
4. `vagrant up` will then create a VM and apply a test playbook (`test.yml`).

You may want to change the base box into one that you like. The current one, [bertvv/centos72](https://atlas.hashicorp.com/bertvv/boxes/centos72) was generated using a Packer template from the [Boxcutter project](https://github.com/boxcutter/centos) with a few modifications.

## Contributing

Issues, feature requests, ideas are appreciated and can be posted in the Issues section. Pull requests are also very welcome. Preferably, create a topic branch and when submitting, squash your commits into one (with a descriptive message).

## License

BSD, see <LICENSE.md>

## Contributors

This role was inspired by the work of [soplakanets](https://github.com/soplakanets/ansible-role-hosts/) (including the [contribution by astrorafael](https://github.com/soplakanets/ansible-role-hosts/pull/1/files)) and [mivok](https://github.com/mivok/ansible-hosts/).

- [Bert Van Vreckem](https://github.com/bertvv/) (maintainer)
- [Dheeraj Dwivedi](https://github.com/dheerajdwivedi)
- [Ernestas Poskus](https://github.com/ernestas-poskus)
- [Mohammed Naser](https://github.com/mnaser)
