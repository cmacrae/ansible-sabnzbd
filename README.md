SABnzbd
=======
This role deploys [SABnzbd](http://sabnzbd.org), an open source binary newsreader.

Requirements
------------
This role requires Ansible 2.0

Supported Platforms
-------------------
- Ubuntu: 15.04
- Debian: 8

Role Variables
--------------
All variables have sensible defaults, which can be found in `defaults/main.yml`.
The current version includes the following variables:

| Name               | Default Value | Description                  |
|--------------------|---------------|------------------------------|
| `sabnzbd_user_name`  | sabnzbd | User to run the SABnzbd service |
| `sabnzbd_group_name` | sabnzbd | Primary group of `sabnzbd_user_name` |
| `sabnzbd_user_uid` | 1005 | UID of the SABnzbd service user |
| `sabnzbd_group_gid` | 1005 | GID of the SABnzbd service group |
| `sabnzbd_user_home` | /var/lib/{{ sabnzbd_user_name }} | home directory for the SABnzbd service user |
| `sabnzbd_library_path` | {{ sabnzbd_user_home }}/data | root library path, to be used for download directories, etc. |
| `sabnzbd_ip` | 0.0.0.0 | IP address the SABnzbd service will listen on |
| `sabnzbd_port` | 8080 | TCP port the SABnzbd web interface will bind to |
| `sabnzbd_clone_uri` | 'git://github.com/sabnzbd/sabnzbd' | The remote SABnzbd Git repo to clone |
| `sabnzbd_follow_git` | false | Ensure SABnzbd source follows HEAD from Git |
| `sabnzbd_dependencies` | - git-core | A list of dependency packages for SABnzbd |
|                        |  - python-cheetah    |  |
|                        |  - python-dbus       |  |
|                        |  - python-openssl    |  |
|                        |  - python-support    |  |
|                        |  - python-yenc       |  |
|                        |  - par2              |  |
|                        |  - unrar-free        |  |
|                        |  - unzip             |  |
|                        |  - p7zip             |  |
| `sabnzbd_service_file` |                      |  |
| `    src`              | sabnzbd.service.j2   | The source template for the SABnzbd service manifest |
| `    dest`             | /etc/systemd/system/sabnzbd.service | The destination to deploy the SABnzbd service manifest to |
| `sabnzbd_service_reload_command` | systemctl daemon-reload | The command used to refresh the SABnzbd service manifest |

Example Playbook
----------------

    - hosts: sabnzbd_servers
      roles:
        - role: cmacrae.sabnzbd

Or, passing parameter values:

	- hosts: sabnzbd_servers
	  roles:
	    - { role: cmacrae.sabnzbd, sabnzbd_user_name: downld, sabnzbd_group_name: downld }
License
-------
MIT

Author Information
------------------
Created by [Calum MacRae](http://cmacr.ae)

Feel free to:  
Contact me - [@calumacrae](https://twitter.com/calumacrae), [mailto:calum0macrae@gmail.com](calum0macrae@gmail.com)  
[Raise an issue](https://github.com/cmacrae/ansible-sabnzbd/issues)  
[Contribute](https://github.com/cmacrae/ansible-sabnzbd/pulls)  
