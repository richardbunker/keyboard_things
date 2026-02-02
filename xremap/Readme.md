1. Download the x86_64 Wayland release from `https://github.com/xremap/xremap/releases`

2. Create systemd user unit at `.config/systemd/user/xremap.service`
```
[Unit]
Description=Run xremap at login
After=graphical-session.target

[Service]
Type=simple
ExecStart=/home/richard/.xremap/run_xremap.sh
Restart=on-failure

[Install]
WantedBy=default.target
```

3. Add run script at `.xremap/run_xremap.sh`
```
#!/bin/bash

sudo /usr/bin/xremap /home/richard/.xremap/caps_to_arrows_dvorak.yml
```

4. Add xremap to sudoers and validate
```
sudo bash -c 'printf "richard ALL=(root) NOPASSWD: /usr/bin/xremap /home/richard/.xremap/caps_to_arrows_dvorak.yml\n" > /etc/sudoers.d/xremap-richard' \
  && sudo chmod 440 /etc/sudoers.d/xremap-richard \
  && sudo visudo -cf /etc/sudoers.d/xremap-richard
```

5. Enter your password when prompted, then log out and log back in
