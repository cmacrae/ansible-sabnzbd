SABnzbd
=======
This role deploys [SABnzbd](http://sabnzbd.org), an open source binary newsreader.

Requirements
------------
This role has been written with [SmartOS](https://smartos.org) in mind, and is designed to be deployed to a [zone](https://wiki.smartos.org/display/DOC/Zones), for use as a server.
However, if popular demand shows, I'll happily add in support for other operating systems.

Role Variables
--------------
All variables have sensible defaults, which can be found in `defaults/main.yml`.
The current version includes the following variables:

| Name               | Default Value | Description                  |
|--------------------|---------------|------------------------------|
| sabnzbd_user_name  | sabnzbd | username to run the SABnzbd service |
| sabnzbd_group_name | sabnzbd | groupname to run the SABnzbd service |
| sabnzbd_user_uid | 1000 | UID of the SABnzbd service user |
| sabnzbd_group_gid | 1000 | GID of the SABnzbd service group |
| sabnzbd_user_home | /opt/{{ sabnzbd_user_name }} | home directory for the SABnzbd service user |
| sabnzbd_conf_path | {{ sabnzbd_user_home }}/.sabnzbd | configuration directory for the SABnzbd service |
| sabnzbd_library_path | {{ sabnzbd_user_home }}/data | root library path, to be used for download directories, etc. |
| sabnzbd_binary_path | {{ sabnzbd_user_home }}/bin/SABnzbd | path where the SABnzbd source will reside |
| sabnzbd_ip | 0.0.0.0 | IP address the SABnzbd service will listen on |
| sabnzbd_port | 8080 | tcp port the SABnzbd web interface will bind to |
| sabnzbd_pid_file | {{ sabnzbd_conf_path }}/sabnzbd-{{ sabnzbd_port }}.pid | pidfile for the SABnzbd service to write the pid to |
| sabnzbd_path_var | /opt/local/bin:/opt/local/sbin:/usr/bin:/bin | set $PATH for the SABnzbd service script |
| sabnzbd_service_args | -f {{ sabnzbd_conf_path }}/settings.ini<br> -b 0 -d --pidfile {{ sabnzbd_pid_file }}<br> -s {{ sabnzbd_ip }}:{{ sabnzbd_port }} | arguments the SABnzbd service will use when starting |
| sabnzbd_source_from_git | False | set to True to grab SABnzbd from Git, rather than a tarball from their site |
| sabnzbd_follow_git | no | ensure SABnzbd source follows HEAD from Git |
| sabnzbd_source_url | (link to SABnzbd source tarball, 0.7.20) | set the source URL for the SABnzbd tarball |
| sabnzbd_source_sha256sum | SHA 256 hashsum of above tarball | set the SHA 256 hashsum to ensure the integrity of the source tarball |

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
