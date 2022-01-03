apt-signing-key
===============

This role allows downloading and adding GPG signing keys
for third-party apt repositories per Debian's recommendations:
https://wiki.debian.org/DebianRepository/UseThirdParty

Requirements
------------

- Debian-based system
- gpg
- wget

Role Variables
--------------

The GPG key is stored under `{{ key_path }}/{{ key_name }}-archive-keyring.gpg` location.

- `url` (required) - GPG key URL.
- `key_name` (required) - GPG key target name.
- `key_path` - Location of archive keyrings. Defaults to the recommended `/usr/share/keyrings`.
- `key_id` - GPG key ID. If provided, the role will redownload a key if it differs from the locally available one.
- `dearmor` - Should the key from the URL be dearmored before saving. Defaults to `false`.

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- name: Provision machine X
  hosts: localhost
  tasks:
    - name: Adding Nodesource signing key
      include_role:
        name: jack1142.apt_signing_key
      vars:
        url: https://deb.nodesource.com/gpgkey/nodesource.gpg.key
        key_name: nodesource
        key_id: 9FD3B784BC1C6FC31A8A0A1C1655A0AB68576280
        dearmor: true
```

License
-------

Apache License 2.0
