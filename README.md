====How to Create Two Network NameSpace in Linux & ping among them====

Run In Root Namespace:

1. Here we will create two namespace; For Create Network nameSpace will Execute Below Command on Cli of root namespace(Host OS);
```bash
 $ ip netns add pc-one
 $ ip netns add pc-two
```
2. To show the created namespace run below command;
```bash
 $ip netns list
```
3. Now we will create link between two virtual Ethernet to connect two network namespace;
```bash
 $ip link add 
  veth-p1 
  type veth
  peer name veth-p2
```
4. To show the created namespace link run below command;
```bash
 $ip link list
```
5. Now we will assign/set the created virtual ethernet with earlier created two NameSpace
```bash
 $ ip link set veth-p1 netns pc-one
 $ ip link set veth-p2 netns pc-two
```
6. Next, will assign the IPs and bring the interfaces up:
```bash
  $ ip netns exec pc-one ip addr add 192.168.0.2/24 dev veth-p1

  $ ip netns exec pc-two ip addr add 192.168.0.3/24 dev veth-p2

  $ ip netns exec pc-one ip link set dev veth-p1 up

  $ ip netns exec pc-two ip link set dev veth-p2 up
```
7. To check the IP address of Network NameSpace we can use the below command;
```bash
  $ ip netns exec pc-one ip ad
```
8. To access both Network NameSpace we can use the below command & will ping from NameSpace to namespace and vice versa;
```bash
  $ip netns exec pc-one bash
  
  $ping 192.168.0.3

  $ip netns exec pc-two bash
  
  $ping 192.168.0.2
```
