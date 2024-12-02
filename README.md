
# TCP Protocol Implementation

> ==Note:== In PCAP++ library, we can copy values from a variable to another just like `pcpp::EthLayer response_eth_layer(tcb.honeypot_mac, tcb.remote_mac,PCPP_ETHERTYPE_IP);` which we created a variable called `response_eth_layer` and copied values from a struct variable `tcb` to the variable `response_eth_layer` and these values are source and destination MAC addresses and the type of ethernet.

After establishing the connection between our honeypot and the sending machine, we go to `handle_established_state` function to handle the connection. ![[Screenshot 2024-11-27 145012.png]]
The function call `create_and_send_new_packet` function to modify our new packet before sending. We will discuss the function `create_and_send_new_packet` in the following part.

----------------------------------------------------------------------
## Receive Data In Established Connection

### Explain The Code

![[Screenshot 2024-11-27 145620.png]]
1. In part 1, we switch the source and destination MAC addresses for our new packet in the ethernet layer and we specify the ethernet type.
2. In part 2, we switch the source and destination IP addresses, set the TTL and the used protocol.
3. In part 3, we modify the ACK number that we will send with the following calculation `Received Seq Number + Number of Received Data Bytes`.
	1. The functions `hostToNet32` and `netToHost32` are used to convert the numbers format from the network and host and vice versa as the host and network have different number formats.

![[Screenshot 2024-11-27 151635.png]]
4. In part 4, we set the our sequence number which is stored in `tcb` struct.
	1. We set the ACK flag, window size, source port and destination port.
5. In part 5, we create a new packet to add the created layers and send the packet.


### Explain Network Traffics

![[Screenshot 2024-11-27 161653.png]]
- We established the connection with our honeypot from my host machine and sent data such as `apple`, `pen` and `book`.

![[Screenshot 2024-11-27 161731 1.png]]
- These are the captured packets using Wireshark tool.
- The first packet with `[PSH, ACK]` flags has a sequence number = 1 and data length = 6, so the following packet has an ACK number = 1 + 6 = 7 and that is important for knowing the packet's order.
- The rest of packets have the same idea.
- **The following screenshots show the sent data in each one of them.** ![[Screenshot 2024-11-27 161838.png]]

![[Screenshot 2024-11-27 161820.png]]

![[Screenshot 2024-11-27 161758.png]]


----------------------------------------------------------------------
## Send Data In Established Connection







----------------------------------------------------------------------
## Connect The Services With The TCP Protocol (Python <==> C++)

- **Potential solutions:**
	- `execlp(file_ptr, arg1_ptr, arg2_ptr, ...., argN_ptr, nullptr);` => Replaces the current process image and it is in the library `unistd.h`.
	- `system("./program arg1 arg2");` is in library `cstdlib`.
	- `execvp()` is used if you don't know the number of arguments beforehand and it is in the library `unistd.h`.

