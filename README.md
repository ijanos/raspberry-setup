# Arch Linux ARM Raspberry Pi 3 - ansible playbook


Follow the
[official installation instructions](https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-3).

Python is required on the target host by Ansible so you have to install that.

```
pacman -S python
```

Check if ansible can reach the pi:

```
ansible all -i 192.168.1.256, -m ping --ask-pass -u alarm
```

Run the playbook.

```
ansible-playbook playbook.yml  -i 192.168.1.256, --ask-pass -u alarm --ask-become-pass --become-method=su
```

The default user is `alarm` the password is `alarm` and the become password is
`root`.


Change the root password and create a password for the newly created user:

```
# passwd USERNAME
```

Then finalize playbook will delete the alarm user and disable password authentication for SSH.

```
ansible-playbook finalize.yml -i 192.168.1.256, --ask-become-pass
```
