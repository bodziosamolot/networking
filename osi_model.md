# Layers

- Layer 7 - Application - HTTP/FTP/gRPC
    - POST request with JSON data to HTTPS server  
- Layer 6 - Presentation - Encoding, Serialization 
    - Serialize JSON to flat byte strings
- Layer 5 - Session - Connection establishment, TLS
    - Request to establish TCP connection/TLS 
- Layer 4 - Transport - UDP/TCP
    - Sends SYN request target port 443
- Layer 3 - Network - IP
    - SYN is placed an IP packet(s) and adds the source/dest IPs 
- Layer 2 - Data link - Frames, Mac address Ethernet
    - Each packet goes into a single frame and adds the source/dest MAC addresses
- Layer 1 - Physical - Electric signals, fiber or radio waves
    - Each frame becomes string of bits which converted into either a radio signal (wifi), electric signal (ethernet), or light (fiber) 