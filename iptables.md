# iptables
## Command Options
|Switch|Meaning|
|---|---|
|-A|Append rule to chain|
|-I|Insert rule at position|
|-D|Delete rule|
|-R|Replace rule|
|-L|List rules|
|-F|Flush (delete all rules)
|-N|Create new chain|
|-X|Delete user-defined chain|
|-P|Set default policy|
|-Z|Zero counters|

## Match Criteria (Filtering)
|Switch|Description|
|---|---|
|-p|Protocol (e.g., tcp, udp, icmp)|
|-s|Source IP address|
|-d|Destination IP address|
|--sport, --dport|Source/Destination port (with -p)|
|-i|Incoming interface|
|-o|Outgoing interface|
|-m|Match extension (e.g. state, conntrack, mac)

## Target Option
|Switch|Meaning|
|---|---|
|-j|**Jump** to target (ACCEPT, DROP, etc.)

### Common targets used with `-j` include:
|Target|Meaning|
|---|---|
|ACCEPT|Allow the packet|
|DROP|Silently discard the packet|
|REJECT|Discard the packet and send and error response|
|LOG|Log the packet info|
|A *user-defined chain name*| Jump to another chain (like a function call)|

Very simple version of firewall configuration to respond with a RST TCP:
```bash
iptables -I input -p tcp --dport <port> -j REJECT --reject-with tcp-reset
```
This can make it extreamly difficult to get an accurate reading of the target.

## Other Options/Administrative
|Switch|Description|
|---|---|
|-v|Verbose output|
|-n|Numeric output (no DNS lookup)|
|--line-numbers|Show line numbers in rule listing|
|-t|Specify the table (filter, nat, mangle, etc|
|--help| Show help iptables|
