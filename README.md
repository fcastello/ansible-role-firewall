# ansible-role-firewall
iptables NAT and firewall configuration for a linux home router.  
This project is to setup a home linux firewall to protect a standard home internet connection, as well as work with masquerade and NAT. The design is simple and allows to add some extra custom rules if needed, however it is very opinionated to solve a specific need by lossing iptables flexibility. If someone needs features just file an issue or submit a pull request witht he changes.  
This role is based from https://github.com/geerlingguy/ansible-role-firewall some ideas and structures were taken from this role. 

# requirements
- ubuntu 18.04. It might work in other ubuntu versions but has been tested with ubuntu 18.04
- iptables: Ubuntu 18.04 alredy has that installed from a minimal install
- systemd:  A basic minimal install of ubuntu 18.04 alredy had systemd installed.


# Limitations
- Only supports on IPv4

# To Do
- Add an easied way to local test/develop using a vagrant vm
- Add support for port forwards to internal hosts
- Add support for port redirections
- Add support for SNAT instead of Masquerade only
- Add ipv6 support
- Add better support for multihomed ISP, Right now is very basic to enable masquerade in multiple interfaces.


# Disclaimer

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE..