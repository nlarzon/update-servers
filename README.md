update-servers
==============

Upgrades all packages on Debian/Ubuntu (`apt dist-upgrade`) and RHEL-family (`dnf`) hosts, then reboots if the OS reports that a reboot is required. Fails on any other OS family.

Requirements
------------

- ansible-core 2.15 or newer
- `become` with sudo on the target hosts
- RedHat hosts: `dnf-plugins-core` (the role installs it) for `dnf needs-restarting`

Role Variables
--------------

Defaults, in `defaults/main.yml`:

| Variable | Default | Meaning |
|---|---|---|
| `update_reboot_allowed` | `true` | Reboot when required. Set `false` to only report it. |
| `update_reboot_timeout` | `600` | Seconds to wait for the host to come back. |
| `update_post_reboot_delay` | `30` | Seconds to wait after boot before continuing. |
| `update_apt_cache_valid_time` | `3600` | Skip `apt update` if the cache is newer than this. |
| `update_autoremove` | `true` | Remove unused dependencies on Debian. |

Tags
----

- `update`: package upgrades and reboot check
- `reboot`: the reboot task. Use `--skip-tags reboot` to patch without rebooting.

Example Playbook
----------------

    - hosts: homelab
      become: true
      serial: 1
      max_fail_percentage: 0
      roles:
        - update-servers

License
-------

MIT-0

Author Information
------------------

nlarzon
