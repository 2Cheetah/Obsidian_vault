# List of users
#linux #users

To see what users are registered in the system, it's needed to check file `/etc/passwd`
```bash
cat /etc/passwd
or
less /etc/passwd
```

Similar output will be provided:
```bash
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
```

Where:
- `root` – Refers to the login name of the user
- `x` – Placeholder or encrypted password; this means the password is stored in a separate file
- `0` – Refers to the user ID. Each user ID is unique per registered user, and in root’s case, it’s user ID is always 0
- `0` – Refers to the group ID, wherein the group ID is also unique for every user
- `root` – Refers to the comment field or a short description of the user
- `/root` – Refers to the home or main directory of users.
- `/bin/bash` – Refers to the user shell that users use to log in the system