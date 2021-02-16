# Google Clouds Logging

## 1. Enable Ansible logging

![Example screenshot](./screens/1.jpg)

## 2. Setup bookshelf app logging to bookshel.log file

![Example screenshot](./screens/2.jpg)

## 3. Created a new configuration files in the additional configuration directory /etc/google-fluentd/config.d and restart agent

```
sudo tee /etc/google-fluentd/config.d/ansible.conf > /dev/null <<EOF
<source>
    @type tail
    <parse>
        # 'none' indicates the log is unstructured (text).
        @type none
    </parse>
    # The path of the log file.
    path /var/log/ansible.log
    # The path of the position file that records where in the log file
    # we have processed already. This is useful when the agent
    # restarts.
    pos_file /var/lib/google-fluentd/pos/ansible.pos
    read_from_head true
    # The log tag for this log input.
    tag ansible
</source>
EOF

sudo tee /etc/google-fluentd/config.d/bookshelf.conf > /dev/null <<EOF
<source>
    @type tail
    <parse>
        # 'none' indicates the log is unstructured (text).
        @type none
    </parse>
    # The path of the log file.
    path /var/log/bookshelf.log
    # The path of the position file that records where in the log file
    # we have processed already. This is useful when the agent
    # restarts.
    pos_file /var/lib/google-fluentd/pos/bookshelf.pos
    read_from_head true
    # The log tag for this log input.
    tag bookshelf
</source>
EOF

```
![Example screenshot](./screens/3.jpg)

## 4. Filter logs in Google Cloud Logging console

![Example screenshot](./screens/4.jpg)
![Example screenshot](./screens/5.jpg)
![Example screenshot](./screens/6.jpg)