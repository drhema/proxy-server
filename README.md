# Squid Proxy Server Setup Script

This script automates the installation and configuration of a Squid proxy server on Ubuntu/Debian systems with user authentication.

## Features

- Automatic installation of required packages
- Interactive setup for port, username, and password
- IPv4 and IPv6 support
- User authentication
- Privacy settings (IP masking)
- Automatic firewall configuration
- Backup of existing configurations
- Detailed success/error reporting
- Test command generation

## Quick Installation

```bash
# Download the script
sudo wget https://gist.github.com/drhema/31652c72c0be1bc43c7d5082bbfe84cd/raw/setup-proxy.sh

# Make it executable
chmod +x setup-proxy.sh

# Run the script
sudo ./setup-proxy.sh
```

## Requirements

- Ubuntu/Debian based system
- Root privileges (sudo)
- Internet connection

## Installation Process

The script will:
1. Install required packages (squid, apache2-utils, curl, net-tools)
2. Prompt for configuration:
   - Port number (1024-65535)
   - Username (alphanumeric characters only)
   - Password (minimum 6 characters)
3. Configure Squid with security settings
4. Set up user authentication
5. Configure firewall rules
6. Start and enable the Squid service

## Configuration

During installation, you'll need to provide:
- Proxy port number (between 1024 and 65535)
- Username (letters, numbers, underscore, hyphen only)
- Password (minimum 6 characters)

## Usage

After installation, you can use the proxy with:
- Host: Your server's IP address
- Port: The port you chose during installation
- Authentication: Username and password you set up

Test the proxy using curl:
```bash
curl -v --proxy-basic --proxy-user username:password -x http://your_server_ip:port http://google.com/
```

## File Locations

- Configuration file: `/etc/squid/squid.conf`
- Password file: `/etc/squid/passwd`
- Cache directory: `/var/spool/squid`
- Log files: `/var/log/squid/`

## Service Management

```bash
# Start Squid
sudo systemctl start squid

# Stop Squid
sudo systemctl stop squid

# Restart Squid
sudo systemctl restart squid

# Check Status
sudo systemctl status squid
```

## Troubleshooting

1. Check service status:
```bash
sudo systemctl status squid
```

2. View logs:
```bash
sudo tail -f /var/log/squid/access.log
sudo tail -f /var/log/squid/cache.log
```

3. Test configuration:
```bash
sudo squid -k parse
```

4. Check port:
```bash
sudo netstat -tulpn | grep squid
```

## Security Considerations

- The script configures basic authentication
- All proxy connections require authentication
- The proxy port is opened in the firewall
- Password file is protected with appropriate permissions
- IP forwarding is disabled for privacy

## Source Code

The complete source code is available at:
https://gist.github.com/drhema/31652c72c0be1bc43c7d5082bbfe84cd

## Support

For issues, please:
1. Check the logs (`/var/log/squid/`)
2. Ensure firewall rules allow the port
3. Verify authentication credentials
4. Check network connectivity

## License

This script is open source and available under the MIT License.

## Contributing

Contributions are welcome:
1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## Updates

Latest update: December 2024
- Added IPv4/IPv6 support
- Improved error handling
- Added firewall configuration
- Enhanced security settings

---
Created by drhema (https://github.com/drhema)
