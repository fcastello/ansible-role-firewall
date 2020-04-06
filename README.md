# ansible-role-firewall
iptables NAT and firewall configuration for a linux home router.  
This project is to setup a home linux firewall to protect a standard home internet connection, as well as work with masquerade and NAT. The design is simple and allows to add some extra custom rules if needed, however it is very opinionated to solve a specific need by lossing iptables flexibility. If someone needs features just file an issue or submit a pull request witht he changes.  
This role is based from https://github.com/geerlingguy/ansible-role-firewall some ideas and structures were taken from this role. 

# requirements
- ubuntu 18.04. It might work in other ubuntu versions but has been tested with ubuntu 18.04
- iptables: Ubuntu 18.04 alredy has that installed from a minimal install
- systemd:  A basic minimal install of ubuntu 18.04 alredy had systemd installed.


# Configuration Variables

```yaml
# Systemd configuration for firewall after running the playbook
firewall_state: started
# enable the systemd unit file to run at boot (usefull to not locking yourself out)
firewall_enabled_at_boot: true
# Set to true to ensure other firewall management software is disabled. This deafults to True to prevent conflicts which will he hard to debug
firewall_disable_ufw: true

# Wether to flush or not all rules before starting to ensure a clean start
firewall_flush_rules_and_chains: true

# Log when packets are being dropped
firewall_log_dropped_packets: false

# Set logging to debug mode.
# BE EXTREMELY CAREFULL WITH THIS AS IT WILL LOG EVERY SINGLE PACKET AND WILL AFFECT PERFORMANCE
# USE ONLY WHEN TESTING AND DEBUGGING
firewall_debug: false

# Enable masquerade 
firewall_enable_masquerade: true
# Enable  packet forwarding in teh kernel
firewall_enable_forwarding: true
# Interfaces to enable masquerade on, neets ennable masqurade to TRUE
firewall_masquerade_interfaces: 
  - "eth1"

## FIREWALL CONFIG
# The firewall config asumes the same rules will apply to INPUT and FORWARD chains. OUTPUT chain will Allow everything as it is the server in question If the is a need for more complex rules they will need to be added to the firewall_additional_rules_pre and firewall_additional_rules_post

# Filtering rules
firewall_allowed_tcp_ports:
  - "22"
firewall_allowed_udp_ports: []

# Redirected ports. This is set for ports to ber redirected to different ports on the same host
firewall_redirected_tcp_ports: 
  - src: "22"
    dst: "2222"
  - src: "80"
    dst: "8080"

firewall_redirected_udp_ports: 
  - src: "53"
    dst: "19053"

# This is a list to add either untrusted hosts or networks. It will deny all traffic to this networks and within this networks
# Should be used when we want to block an external host that is attaking us. This will be the rules evaluated on top of every other rules to block at the earliest
# Casn use a single ip or a subnet in CIDR notation
firewall_blacklist: []

# This is a list to add either trusted hosts or networks. It will allow all traffic to this networks and within this networks
# useful to add all internal private networks
# Casn use a single ip or a subnet in CIDR notation
firewall_whitelist: []

# Example: Whitelist all common private subnets
# firewall_whitelist: 
#   - 192.168.0.0/16
#   - 10.0.0.0/8
#   - 172.16.0.0/12

## Custom Rules
# Custom rules are used to define the raw iptables rules when needing special use cases, 
# NOTE: you will have to specify the entire iptables command in order to work

# Additional rules are custom rules to be applied before the standarrd rules
firewall_additional_rules_pre: []

# Additional rules are custom rules to be applied after the standarrd rules
firewall_additional_rules_post: []
```


# Limitations
- Only supports on IPv4

# To Do
- Add an easied way to local test/develop using a vagrant vm
- Add support for port forwards to internal hosts
- Add support for SNAT instead of Masquerade only
- Add ipv6 support
- Add better support for multihomed ISP, Right now is very basic to enable masquerade in multiple interfaces.


# Disclaimer

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.