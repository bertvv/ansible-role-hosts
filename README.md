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

| Variable                          | Default | Comments                                                                                                                                      |
| :---                              | :---    | :---                                                                                                                                          |
| `hosts_add_default_ipv4`          | true    | If true, an entry for the host name is added, bound to the host's default IPv4 address.                                                       |
| `hosts_add_basic_ipv6`            | false   | If true, basic IPv6 entries are added (e.g. localhost6, ip6-localnet, etc.)                                                                   |
| `hosts_add_ansible_managed_hosts` | false   | If true, an entry for hosts managed by Ansible is added. This includes the current host, so this makes `hosts_add_default_ipv4` unneccessary. |
| `hosts_entries`                   | []      | A list of dicts with custom entries to be added to the hosts file. See below for an example.                                                  |
| `hosts_file_snippets`             | []      | A list of files containing host file snippets to be added to the hosts file verbatim.                                                         |

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

See the [test playbook](tests/test.yml)

## Testing

The `tests` directory contains tests for this role in the form of a Vagrant environment. The playbook [`test.yml`](tests/test.yml) applies the role to a VM, setting all role variables.

The directory `tests/roles/hostsfile` is a symbolic link that should point to the root of this project in order to work. To create it, do

```ShellSession
$ cd tests/
$ mkdir roles
$ ln -frs ../../PROJECT_DIR roles/hostsfile
```

You may want to change the base box into one that you like. The current one is based on Box-Cutter's [CentOS Packer template](https://github.com/boxcutter/centos).


## Contributing

Issues, feature requests, ideas are appreciated and can be posted in the Issues section. Pull requests are also very welcome. Preferably, create a topic branch and when submitting, squash your commits into one (with a descriptive message).

## License

BSD, see <LICENSE.md>

## Author Information

Bert Van Vreckem (bert.vanvreckem@gmail.com)

Inspired by similar roles by [soplakanets](https://github.com/soplakanets/ansible-role-hosts/) (including the [contribution by astrorafael](https://github.com/soplakanets/ansible-role-hosts/pull/1/files)) and [mivok](https://github.com/mivok/ansible-hosts/).
