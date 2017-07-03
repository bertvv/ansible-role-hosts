# Change log

This file contains al notable changes to the hosts Ansible role.

This file adheres to the guidelines of [http://keepachangelog.com/](http://keepachangelog.com/). Versioning follows [Semantic Versioning](http://semver.org/).

## 1.2.0 - 2017-07-03

### Added

- (GH-3) Added host file backup flag (Credit: [Dheeraj Dwivedi](https://github.com/dheerajdwivedi))

## 1.1.0 - 2016-05-31

### Added

- (GH-2) Allow setting the network interface and IP protocol when adding entries for Ansible managed hosts. (credit: [Ernestas Poskus](https://github.com/ernestas-poskus))


## 1.0.2 - 2016-05-21

### Changed

- Fixed Ansible 2.0 deprecation warnings in role (GH-1) and test code. (partial credits to [Ernestas Poskus](https://github.com/ernestas-poskus))

## 1.0.1 - 2015-08-18

### Changed

- When adding entries for Ansible managed hosts, skip hosts that do not have `ansible_default_ipv4` set.

## 1.0.0 - 2015-07-30

First release!

### Added

- Host file template
- Add the default localhost entry;
- Add an entry for the host name bound to the host's default external IPv4 address (optional);
- Add entries for basic IPv6 addresses, e.g. ip6-localnet (optional);
- Add entries for Ansible managed hosts (optional);
- Add entries specified in Yaml (optional);
- Add entries specified in text files (optional).

