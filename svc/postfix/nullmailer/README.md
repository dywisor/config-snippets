Notes
-----

postfix config that sends all mails to one or more upstream SMTP servers.
Local user addresses are partially rewritten
(envelope sender/rcpt, not From header -- and not all users).

```
debconf-set-selections <<EOF
postfix postfix/main_mailer_type select No configuration
EOF

apt install postfix

# install postfix config
# - /etc/postfix/master.cf
#   disable smtp smtpd, virtual, lmtp, uucp
# - /etc/postfix/main.cf
#   - adjust the following vars:
#     - myorigin
#     - myhostname
#     - smtp_helo_name (optional)
#     - relayhost
# - /etc/postfix/aliases
#   - add mail users
# - /etc/postfix/sender_canonical
#   - add mail users

newaliases

postmap /etc/postfix/sender_canonical

postfix check

systemctl restart postfix
systemctl enable postfix
```
