# Kill switch

```sh
# Environment setup
export LAN_MASK=""
export VPN_IP=""
export VPN_PROTOCOL=""
export VPN_PORT=""

# Disable IPv6
echo "net.ipv6.conf.all.disable_ipv6=1" | sudo tee -a /etc/sysctl.conf
echo "net.ipv6.conf.default.disable_ipv6=1" | sudo tee -a /etc/sysctl.conf
echo "net.ipv6.conf.lo.disable_ipv6=1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
cat /proc/sys/net/ipv6/conf/all/disable_ipv6 # confirm if 1

# Disable IPv6 on ufw
sudo sed -i "s/IPV6=yes/IPV6=no/g" /etc/default/ufw

# Allow LAN traffic
sudo ufw allow in to $LAN_MASK && sudo ufw allow out to $LAN_MASK

# VPN kill switch
sudo ufw default deny outgoing && sudo ufw default deny incoming
sudo ufw allow out to $VPN_IP port $VPN_PORT proto $VPN_PROTOCOL
sudo ufw allow out on tun0 from any to any && sudo ufw allow in on tun0 from any to any

# Enable ufw
sudo ufw enable

# Confirm ufw status
sudo ufw status
```
