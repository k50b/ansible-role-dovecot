Ansible role: Dovecot
=====================

Basic dovecot installation with submission protocol support.

Features:

1. Handles IMAP protocol and authenticated mail submission through SMTP on port 587.
2. Creates an empty users file `/etc/dovecot/users` which have to be configured according to the `passwd-file` format \[0\].
3. System's PAM authentication is disabled is disabled in `10-auth.conf` and only passwd-file is left enabled.
4. Mailbox path is configured in `10-mail.conf` to be `{{ dovecot_mailbox_root_dir }}/%d/%n`. For example for `test@example.com` account and `{{ dovecot_mailbox_root_dir }} = /home/vmail` the path will be `/home/vmail/example.com/test`. Mail Delivery Agent have to be configured in the same way to deliver messages to the correct mailbox. Postfix for example can be configured with `virtual_mailbox_base` and `virtual_mailbox_maps` \[1\] options.

\[0\]: Passwd-file file format description: https://doc.dovecot.org/configuration_manual/authentication/passwd_file/

\[1\]: http://www.postfix.org/VIRTUAL_README.html#virtual_mailbox

Requirements
------------

- Mail Delivery Agent (eg. Postfix). Dovecot's submission handler will pass received message to the SMTP server.

Role Variables
--------------

```
dovecot_mailbox_root_dir: /home/vmail
dovecot_cert_path: /etc/ssl/certs/ssl-cert-snakeoil.pem
dovecot_privkey_path: /etc/ssl/private/ssl-cert-snakeoil.key
dovecot_submission_hostname: mail.example.com
```

Example Playbook
----------------



License
-------

MIT