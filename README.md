# fstab

This Role generates a proper apt sources.


## Requirements

A running debian based system.


## Role Variables

| Name                                    | Type                                 | Description                                                                                                                                                                       |
|-----------------------------------------|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `apt_sources_ubuntu`                    | [dict](#apt_sources_ubuntu) | Apt source config for ubuntu systems                                                                                                                                              |
| `apt_sources_debian`                    | [dict](#apt_sources_debian) | Apt source config for debian systems                                                                                                                                              |
| `apt_sources_additional_source_strings` | list of strings                      | Additional apt sources to add (each string is additional line in `/etc/apt/sources.list` without any modifications)(This option will be overwritten by the release specific ones) |


### apt_sources_ubuntu
| Option Key                  | Type            |  Default/Required [¹](#__required)   | Description                                                                                                         |
|-----------------------------|-----------------|:------------------------------------:|---------------------------------------------------------------------------------------------------------------------|
| `release`                   | string          | `{{ ansible_distribution_release }}` | Release string to set                                                                                               |
| `mirror`                    | string          |    `http://de.archive.ubuntu.com/`   | Mirror to use for apt entries (The leading `/` is required)                                                         |
| `enable_sources`            | boolean         |                `False`               | Enable `deb-src` entries                                                                                            |
| `components`                | list of strings |        `['main', 'universe']`        | Components to enable (valid values are: `main`, `restricted`, `universe`, `multiverse`)                             |
| `security_repo`             | boolean         |                `True`                | Enable security repository                                                                                          |
| `update_repo`               | boolean         |                `True`                | Enable general update repository                                                                                    |
| `backports`                 | boolean         |                `False`               | Enable backports repository                                                                                         |
| `proposed`                  | boolean         |                `False`               | Enable proposed repository                                                                                          |
| `canonical`                 | boolean         |                `False`               | Enable ubuntu partner (canonical) repository                                                                        |
| `canonical_mirror`          | string          |    `http://archive.canonical.com/`   | Ubuntu canonical mirror to use                                                                                      |
| `additional_source_strings` | list of strings |                 `[]`                 | Additional apt sources to add (each string is additional line in `/etc/apt/sources.list` without any modifications) |

<a id="__required">¹</a> Variable is not required unless no default is given or other specified


### apt_sources_debian
| Option Key                  | Type            |  Default/Required [¹](#__required)   | Description                                                                                                         |
|-----------------------------|-----------------|:------------------------------------:|---------------------------------------------------------------------------------------------------------------------|
| `release`                   | string          | `{{ ansible_distribution_release }}` | Release string to set                                                                                               |
| `mirror`                    | string          |      `http://ftp.de.debian.org/`     | Mirror to use for apt entries (The leading `/` is required)                                                         |
| `enable_sources`            | boolean         |                `False`               | Enable `deb-src` entries                                                                                            |
| `components`                | list of strings |         `['main', 'contrib']`        | Components to enable (valid values are: `main`, `contrib`, `non-free`)                                              |
| `security_repo`             | boolean         |                `True`                | Enable security repository                                                                                          |
| `update_repo`               | boolean         |                `True`                | Enable general update repository                                                                                    |
| `backports`                 | boolean         |                `False`               | Enable backports repository                                                                                         |
| `additional_source_strings` | list of strings |                 `[]`                 | Additional apt sources to add (each string is additional line in `/etc/apt/sources.list` without any modifications) |


## Example Configuration

```yml
apt_sources_debian:
  mirror: http://ftp.us.debian.org/

apt_sources_ubuntu:
  components:
    - main
    - restricted
    - universe
    - multiverse
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

- [Markus Mroch (Mr. Pi)](https://github.com/Mr-Pi) _markus.mroch@stuvus.uni-stuttgart.de_
