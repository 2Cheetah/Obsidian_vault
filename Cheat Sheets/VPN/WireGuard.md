# WireGuard VPN
#VPN #wireguard

[WireGuard VPN — лучше платных сервисов и проще OpenVPN. Полная настройка WireGuard! - YouTube](https://www.youtube.com/watch?v=5Aql0V-ta8A&ab_channel=%D0%94%D0%B8%D0%B4%D0%B6%D0%B8%D1%82%D0%B0%D0%BB%D0%B8%D0%B7%D0%B8%D1%80%D1%83%D0%B9%21)

## Add new users

On server:
- Switch to folder `/etc/wireguard`
- Create *private* and *public* keys:
```bash
wg genkey | tee /etc/wireguard/monster_win_privatekey | wg pubkey | tee /etc/wireguard/monster_win_publickey
```

- Update `wg0.conf` file, add new `peer`. Assign internal IP address to the peer, here it is `<peer IP>/32`. Public key can be taken from output of previous step:
```text
[Peer]
PublicKey = <peer public key>
AllowedIPs = <peer IP>/32
```

- Restart WireGuard service and check if it works:
```bash
systemctl restart wg-quick@wg0.service
systemctl status wg-quick@wg0.service
```
On local machine:
- Create a configuration file. Can be a copy of existing configuration:
```text
[Interface]
PrivateKey = <peer private key>
Address = <peer IP>/32
DNS = 8.8.8.8

[Peer]
PublicKey = <server public key>
AllowedIPs = 0.0.0.0/0
Endpoint = <server IP>:<port>
PersistentKeepalive = 20
```

- Add that configuration file to the WireGuard client.