Wire protocols are generally built on top of tcp (they live in the application layer, like http)
interesting differences from http, postgres is stateful, meaning each side (?) holds the state of the transactions.

2 phases of connection:
- on startup, the driver makes the connect() kernel call and performs the tcp handshake with the server. this means the driver must be part of the application/running in the same process.
	- http based APIs also exist, where your app makes http requests to a remote service where the driver runs.
- after the connection is active, there are two protocols for sending queries:
	- **simple query** protocol
	- **extended query** protocol

