# WireGuard VPN Management Scripts Guide

This guide provides detailed instructions on using the WireGuard VPN management scripts installed on your server. The scripts make it easy to add and remove clients, manage Mac configurations, and ensure your VPN stays reliable.

## Available Scripts

Your WireGuard server includes four management scripts:

1. **add_wireguard_peer** - Adds a new client to your VPN
2. **remove_wireguard_peer** - Removes a specific client from your VPN
3. **remove_all_wireguard_peers** - Removes all clients from your VPN
4. **mac_wireguard_config** - Prepares client configurations for Mac users
5. **wireguard-maintenance** - Ensures WireGuard stays up and running

## Quick Reference

| Task | Command |
|------|---------|
| Add new client | `sudo add_wireguard_peer client_name 10.0.0.x` |
| Remove client | `sudo remove_wireguard_peer 10.0.0.x` |
| Remove all clients | `sudo remove_all_wireguard_peers` |
| Generate Mac config | `sudo mac_wireguard_config client_name` |
| Manually run maintenance | `sudo wireguard-maintenance` |
| Check VPN status | `sudo wg show` |

## Detailed Instructions

### 1. Adding a New Client

The `add_wireguard_peer` script creates a new VPN client with the specified name and IP address.

**Usage:**
```bash
sudo add_wireguard_peer CLIENT_NAME CLIENT_IP
```

**Example:**
```bash
sudo add_wireguard_peer laptop 10.0.0.5
```

This will:
- Generate encryption keys for the new client
- Create a client configuration file
- Add the client to the server
- Display a QR code for mobile setup

**Available IP Addresses:**
Your VPN subnet (10.0.0.0/24) provides 253 usable client IP addresses:
- 10.0.0.1 is used by the server
- You can assign clients from 10.0.0.2 to 10.0.0.254

**Client Naming Tips:**
- Use descriptive names without spaces
- Examples: laptop, phone, work, home, ipad

After running the command, scan the QR code with the WireGuard mobile app or use the configuration file for desktop clients.

### 2. Removing a Specific Client

The `remove_wireguard_peer` script revokes access for a specific client.

**Usage:**
```bash
sudo remove_wireguard_peer CLIENT_IP
```

**Example:**
```bash
sudo remove_wireguard_peer 10.0.0.5
```

This will:
- Immediately disconnect the client
- Remove the client from the server configuration
- Delete the client's configuration files

### 3. Removing All Clients

The `remove_all_wireguard_peers` script removes all VPN clients, giving you a clean slate.

**Usage:**
```bash
sudo remove_all_wireguard_peers
```

This will:
- Ask for confirmation before proceeding
- Remove all clients from your VPN
- Delete all client configuration files
- Keep your server configuration intact

**Warning:** This immediately revokes access for all clients. They will need to be reconfigured to regain VPN access.

### 4. Setting Up Mac Clients

The `mac_wireguard_config` script prepares WireGuard configurations for Mac users.

**Usage:**
```bash
sudo mac_wireguard_config CLIENT_NAME
```

**Example:**
```bash
sudo mac_wireguard_config macbook
```

This will:
- Create a downloadable configuration file
- Generate a Base64 encoded string for clipboard transfer
- Provide instructions for importing on a Mac

**Setup Steps for Mac Users:**
1. Install the WireGuard client from the Mac App Store
2. Choose one of the provided transfer options:
   - SCP command to download the file directly
   - Base64 string to copy/paste
3. Import the configuration into the WireGuard app

### 5. Ensuring VPN Reliability

The `wireguard-maintenance` script keeps your VPN running properly.

**Usage:**
```bash
sudo wireguard-maintenance
```

This script:
- Checks if WireGuard is running and starts it if needed
- Ensures WireGuard starts on boot
- Verifies correct firewall settings
- Checks for and applies updates
- Logs all activities to `/var/log/wireguard-maintenance.log`

It runs automatically through a cron job:
- Daily at 3:00 AM for routine maintenance
- Every 15 minutes to check if WireGuard is running

You can run it manually anytime to ensure everything is working properly.

## Checking VPN Status

To check the status of your WireGuard VPN and see connected clients:

```bash
sudo wg show
```

This will display:
- All configured clients
- Their public keys
- Their allowed IP addresses
- Latest handshake times (when they last connected)
- Data transfer statistics

## Choosing Client IP Addresses

Your VPN subnet (10.0.0.0/24) provides 254 IP addresses:
- 10.0.0.0 = Network address (not usable)
- 10.0.0.1 = Server address
- 10.0.0.2 - 10.0.0.254 = Available for clients
- 10.0.0.255 = Broadcast address (not usable)

Consider organizing client IPs by device type or location:
- 10.0.0.2-10: Main devices
- 10.0.0.11-20: Mobile devices
- 10.0.0.21-30: Home devices
- 10.0.0.31-40: Work devices

## Troubleshooting

If you encounter issues with the scripts or VPN connections:

1. **Check VPN status:**
   ```bash
   sudo wg show
   ```

2. **View WireGuard logs:**
   ```bash
   sudo journalctl -u wg-quick@wg0
   ```

3. **Check maintenance logs:**
   ```bash
   sudo cat /var/log/wireguard-maintenance.log
   ```

4. **Verify firewall settings:**
   ```bash
   sudo ufw status
   ```

5. **Restart WireGuard:**
   ```bash
   sudo systemctl restart wg-quick@wg0
   ```

## Additional Resources

- [Official WireGuard Documentation](https://www.wireguard.com/quickstart/)
- [WireGuard Client Downloads](https://www.wireguard.com/install/)
