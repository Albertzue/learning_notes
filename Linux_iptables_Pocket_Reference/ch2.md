# iptables Command Reference
[link](https://learning.oreilly.com/library/view/linux-iptables-pocket/9780596801861/ch01s02.html#iptables_miscellaneous_options)

# Getting help
iptables provides some online help. You can get basic information via these commands:
```
iptables -h
iptables -m match -h
iptables -j TARGET -h
man iptables
```

# The iptables Subcommands
Each iptables command can contain one subcommand, which performs an operation on a particular table (and, in some cases, chain)
[link](https://learning.oreilly.com/library/view/linux-iptables-pocket/9780596801861/ch01s02.html#iptables_subcommand_options)

# iptables Matches and Targets
iptables has a small number of built-in matches and targets, and a set of extensions that are loaded if they are referenced.
The matches for IP are considered built-in, and the others are considered match extensions 
(even though the icmp, tcp, and udp match extensions are automatically loaded when the corresponding protocols are referenced with the -p built-in Internet Protocol match option).
