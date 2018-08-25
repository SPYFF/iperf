# iperf3 with IPv6 Segment Routing support

Very fragile yet working IPv6 segment routing support for iperf3. You could measure the throughput of detoured paths.
**Implemented as a project at ACM SIGCOMM 2018 Hackathon**

### Example
```
                  fc02::2:2
                   +----+
               +---+ R2 +---+
               |   +----+   |
               |            |
fc02::1:1      |            |      fc02::3:3
+------+     +-+--+      +--+-+     +------+
|Client+-----+ R1 +------+ R3 +-----+Server|
+------+     +----+      +----+     +------+

```

If you want to measure the throughput between client and server node, normally the traffic goes through the **R1** and **R3** routers between them. But with IPv6 Segment routing you can specify the exact path even if that contains a detour like **R2**. 

For regular measurement you could run the folling command (assuming iperf3 server running on host **Server**)
```
iperf3 -c fc02::3:3
```
Instead if the intermediate nodes have segment routing support, you can detour the TCP flow to **R1->R2->R3** path:
```
iperf3 -c fc02::2:2,fc02::3:3
```
Possible to add even more segment as before in more complex topologies
```
iperf3 -c 2001::ab54:2,2002:342F::b889,fc02::88:75,fc02::34C
```

### TODO

- [x] Basic functioning implementation 
- [ ] Proper error handling
- [ ] JSON parsing
- [ ] Reverse path support (like `iperf3 -c fc02::5 -R`)

================================================================

Informations about the compilation and install, check the regular iperf3 docs.
