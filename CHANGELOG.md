# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).


## [1.0.0] - 2020-08-28
### Added
- Support for IPv6
- BREAKING CHANGE - Following configuration varieables have been namespaced to support IPv6 - firewall_redirected_tcp_ports, firewall_redirected_udp_ports, firewall_forwarded_tcp_ports, firewall_forwarded_udp_ports, firewall_blacklist, firewall_whitelist. Refer to the defaults/main.yml file for reference how to use the variables.

## [0.3.1] - 2020-08-23
### Fixed
- Bug where playbook failed when trying to disable ufw and ufw was not installed

## [0.3.0] - 2024-08-17
### Fixed
- Updated supported ansible version
- Updated disabling firewall scripts to use systemd
- Linting errors

## [0.2.0] - 2020-04-06
### Added 
- Port forwards

## [0.1.1] - 2020-04-06
### Fixed 
- Port redirection variable with wrong name

## [0.1.0] - 2020-04-05
### Added 
- Port redirection

## [0.0.3] - 2020-03-22
### Changed
- Minor fixes in formating and removing trailing spaces
### Removed
- Testing travis CI configuration

## [0.0.2] - 2020-03-22
### Added
- Testing travis CI configuration

## [0.0.1] - 2020-03-22 -  Initial commit
### Added
- First iteration of the role