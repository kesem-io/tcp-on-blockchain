# tcp-on-blockchain
"**TCP On Blockchain**" or "**Redesign TCP with Blockchain technology**"

# Abstract summary
Today, the Blockchain become very popular topic in the computer industry. In this paper I will try to combine this popular technology with the backbone technology of the Internet – a TCP protocol.

In a nutshell, the Blockchain technology talks about creating chain of messages/blocks. Each block consists of a hash of the previous block coupled with some data. The data can be for example transactions. Blockchain implementation uses special hash function. No one can change the blocks that are already in the chain, without recalculating all aftermath blocks hashes.

![Blockchain](https://raw.githubusercontent.com/kesem-io/tcp-on-blockchain/master/blocks.png)

One of the known issues with TCP protocol is **Man-In-The-Middle attack** (**MITM**). **MITM** is an attack where the attacker secretly relays and possibly alters the communication between two parties who believe they are directly communicating with each other. There are 2 possible scenarios for **TCP** – a proxy usage; and overtaking of the existing TCP connection.

In this document, I will not address the scenario of the proxy usage – when the attacker can recreate a totally new connection and proxy user requests. The SSL private keys is made to protect from it.

On the contrary, I will show a way to stop active TCP connection overtaking without any encryption by combining TCP with Blockchain technology. In order to be able to do so, I will need to add another algorithm to the mash. It is called **Diffie-Hellman-Merkle algorithm**. It’s beauty is that encryption key or a session key is created over totally untrusted channel, meaning, it can be done in clear text.

# New TCP protocol based on Blockchain

In original **TCP** protocol, each party sends **SEQ** and **ACK** numbers to the opposite party. **SEQ** stands for packet sequence. It grows, on each to packet from side A to side B. **ACK** stands for packet acknowledgement. It is equal to the last **SEQ** packet received from side B plus packet data size.

In a new **TCP** protocol, instead of **SEQ** numbers, we will use **HASH** values.

# Session key
Each side, will submit to the opposite side special numbers required to establish common master key. The attacker, looking on the packets, will not be able to calculate this session key. It is all due to **Diffie-Hellman-Merkle algorithm**.

# HASH calculations
On each new packet, the sender will calculate hash value using the following formula:

**HASH** = hash(prev_hash_value, data, session_key)

**Prev_hash_value** specifies previous hash value generated by the same party.
**Data** is actual data inside packet. For example “GET /” for web request.
**Session_key** – is a session key as calculated.

# TCP ACKnowledgement
TCP ACK will be equal to the latest valid hash value as received from other party.

# Packet validation
Upon receiving a packet, the receiving side, will extract packet **HASH** and **ACK** values.
It will check that the **HASH** of the received packet is correct using the following formula:

**HASH** = hash(prev_opposite_hash_value, received_data, session_key)

**Prev_oppisite_hash_value** specifies previous hash value received from other party.
**Received_data** is actual data inside packet received.
**Session_key** – is a session key calculated.

If the calculated **HASH** value is equal to the one shown in the packet header, it is considered as legitimate packet and the new **HASH** value is remembered and used as **ACKnowledgement** number.
