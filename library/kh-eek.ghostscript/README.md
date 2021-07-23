Role Name
=========

Ansible role to install GhostScript

Requirements
------------

No

Role Variables
--------------
A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

  gs_major_version: 9

GhostScript major version number

  gs_minor_version: 21

GhostScript minor version number

  gs_archive: "ghostscript-{{ gs_major_version }}.{{ gs_minor_version }}"

GhostScript archive file name

  gs_archive_checksum:

GhostScript archive SHA256 checksum

  gs_archive_dir: "/tmp/{{ gs_archive }}.tar.gz"

GhostScript archive download directory

  gs_unarchive_dir: "/tmp/{{ gs_archive }}"

GhostScript unarchive download directory

  gs_fonts_install: false

If you install GhostScript fonts

  gs_fonts_download_url: "https://nchc.dl.sourceforge.net/project/gs-fonts/gs-fonts/8.11%20%28base%2035%2C%20GPL%29/ghostscript-fonts-std-8.11.tar.gz"

GhostScript fonts download URL

  gs_fonts_archive: ghostscript-fonts-std-8.11.tar.gz

GhostScript fonts archive name



Dependencies
------------

No

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: kh-eek.ghostscript }

License
-------

BSD

Author Information
------------------
Sida Say (sidasay@kheek.com)
