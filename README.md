# tcp-on-blockchain
"**TCP On Blockchain**" or "**Redesign TCP with Blockchain technology**"

Today, the Blockchain become very popular topic in the computer industry. In this paper I will try to combine this popular technology with the backbone technology of the Internet – a TCP protocol.

In a nutshell, the Blockchain technology talks about creating chain of messages/blocks. Each block consists of a hash of the previous block coupled with some data. The data can be for example transactions. Blockchain implementation uses special hash function. No one can change the blocks that are already in the chain, without recalculating all aftermath blocks hashes.

One of the known issues with TCP protocol is **Man-In-The-Middle attack** (**MITM**). **MITM** is an attack where the attacker secretly relays and possibly alters the communication between two parties who believe they are directly communicating with each other. There are 2 possible scenarios for **TCP** – a proxy usage; and overtaking of the existing TCP connection.

In this document, I will not address the scenario of the proxy usage – when the attacker can recreate a totally new connection and proxy user requests. The SSL private keys is made to protect from it.

On the contrary, I will show a way to stop active TCP connection overtaking without any encryption by combining TCP with Blockchain technology. In order to be able to do so, I will need to add another algorithm to the mash. It is called **Diffie-Hellman-Merkle algorithm**. It’s beauty is that encryption key or a session key is created over totally untrusted channel, meaning, it can be done in clear text.
