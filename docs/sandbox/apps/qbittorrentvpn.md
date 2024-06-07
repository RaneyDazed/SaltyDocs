# qBittorrentvpn

## What is it?

[qbittorrentvpn](https://github.com/binhex/arch-qbittorrentvpn) is a qbittorrent container which includes OpenVPN and WireGuard to ensure a secure and private connection to the Internet, including use of iptables to prevent IP leakage when the tunnel is down. It also includes Privoxy to allow unfiltered access to index sites.

| Details     |             |             |             |
|-------------|-------------|-------------|-------------|
| [:material-home: Project home](https://github.com/binhex/arch-qbittorrentvpn){: .header-icons } | [:octicons-link-16: Docs](https://github.com/binhex/arch-qbittorrentvpn){: .header-icons } | [:octicons-mark-github-16: Github](https://github.com/binhex/arch-qbittorrentvpn){: .header-icons } | [:material-docker: Docker](https://hub.docker.com/r/binhex/arch-qbittorrentvpn){: .header-icons }|

### 1. Installation

In `/opt/sandbox/settings.yml`, adjust the following:

``` yaml title="/opt/sandbox/settings.yml"

qbittorrentvpn: # (1)!
  vpn_pass: your_vpn_password # (2)!
  vpn_prov: pia # (3)!
  vpn_user: your_vpn_username # (4)!
  vpn_client: wireguard # (5)!

```

1. This is the name of the role.
2. This is the password for your VPN provider.
3. This is the name of your VPN provider.
4. This is the username for your VPN provider.
5. This is the client you want to use for your VPN provider.

As described in the github readme linked above, then run the role:

``` shell

sb install sandbox-qbittorrentvpn

```

### 2. URL

- To access qbittorrentvpn, visit `https://qbittorrentvpn._yourdomain.com_`

### 3. Setup

- [:octicons-link-16: Documentation: qBittorrentvpn Docs](https://github.com/binhex/arch-qbittorrentvpn){: .header-icons }
