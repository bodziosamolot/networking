# TLS

- Transport Level Security
- Transport layer (Layer 4) concern

# TLS vs HTTPS

TLS is a cryptographic protocol that secures communication between systems, while HTTPS is a secure version of the HTTP protocol that uses TLS to encrypt data transmitted between a client (browser) and a server (website). In essence, TLS provides the security layer, and HTTPS is an implementation of that security for web applications.

- When using HTTPS with ASP.NET it is not the framework that is responsible for encryption. Encryption is the responsibility of the server. That means that Kestrel is doing the encryption.
- Kestrel, like other web servers, negotiates a secure connection with the client using the TLS/SSL protocol. This involves exchanging cryptographic keys, agreeing on cipher suites, and establishing an encrypted communication channel. Once the secure channel is established, all data transmitted between the client and the server is encrypted, ensuring confidentiality and integrity.