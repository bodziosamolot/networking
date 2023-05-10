# DNS

- Domain Name System
- Built on UDP
- Uses port 53
- Finds out what is the IP (or set of ip addresses) address matching a domain name so that we can use TCP
- Why do we need domain names?
    - Names are easier to remember than ip addresses
    - Ip address can change but the domain name remains
- www.onet.pl
    - www - subdomain
    - onet - domain
    - pl - top level domain
- Can provide the IP of the geographicaly closes server
- Record types:
    - A (Address) record: Maps a domain name to an IPv4 address. This is the most basic and common type of DNS record.
    - AAAA (Address) record: Similar to an A record, but it maps a domain name to an IPv6 address instead.
    - CNAME (Canonical Name) record is a type of DNS record that maps one domain name (an alias) to another domain name (the canonical name). It's used when you want to associate an additional subdomain or domain name with an existing domain, without having to maintain separate DNS records for each. Using a CNAME record typically results in an additional DNS roundtrip. When a client requests the IP address of a domain name that has a CNAME record, the following steps occur:
        1. The client sends a DNS query for the domain name with the CNAME record (the alias).
        2. The DNS resolver returns the CNAME record, which contains the canonical domain name that the alias points to.
        3. The client sends another DNS query for the canonical domain name.
        4. The DNS resolver returns the A or AAAA record for the canonical domain name, providing the IP address.
    - MX (Mail Exchange) record: Directs email traffic to a specific mail server responsible for handling email for a domain. It contains a preference value, which helps prioritize mail servers if multiple MX records are present.
    - TXT (Text) record: Holds arbitrary text information. Often used for various verification purposes, such as SPF (Sender Policy Framework) and DKIM (DomainKeys Identified Mail) records, which help prevent email spoofing and improve email deliverability.
    - NS (Name Server) record: Specifies the authoritative name servers responsible for a domain. These servers hold the DNS records for the domain and respond to DNS queries.
    - PTR (Pointer) record: Provides reverse DNS lookups, allowing you to resolve an IP address back to a domain name. Typically used for reverse DNS zones and email server identification.
    - SRV (Service) record: Defines the location and priority of specific services, such as VoIP or instant messaging, within a domain. It contains the hostname, port, priority, and weight of the service.
    - SOA (Start of Authority) record: Contains important information about a DNS zone, such as the primary name server, the email address of the domain administrator, and the zone's serial number. This record helps manage and synchronize DNS information across multiple name servers.
    - CAA (Certification Authority Authorization) record: Specifies which certificate authorities (CAs) are allowed to issue SSL/TLS certificates for a domain. This helps improve security by preventing unauthorized CAs from issuing certificates for your domain.
- If we had all ip addresses in a single data store, then the index would be huge. That's why dns entries have to be partitioned:
    - Root Servers: These servers sit at the top of the DNS hierarchy and are the starting point for resolving domain names. They maintain information about the top-level domains (TLDs) and their corresponding authoritative name servers. There are 13 root server clusters, named from A to M, managed by different organizations and distributed worldwide.
    - Top-Level Domain (TLD) Servers: TLD servers are responsible for managing the second level of the DNS hierarchy, which includes generic TLDs (gTLDs) such as .com, .org, .net, and country-code TLDs (ccTLDs) like .us, .uk, .de, etc. They store information about the authoritative name servers for each second-level domain under their respective TLD.
    - Authoritative Name Servers: These servers hold the actual DNS records (A, AAAA, CNAME, MX, etc.) for a specific domain or set of domains. They are considered the authoritative source for DNS information about those domains. When a DNS resolver receives a query for a domain, it ultimately communicates with the authoritative name server to obtain the requested information.
    - Recursive Resolvers (also called DNS Resolvers or Caching Servers): These servers act as intermediaries between clients and the DNS hierarchy. They receive DNS queries from clients, then recursively navigate through the DNS hierarchy—from root servers to TLD servers to authoritative name servers—to resolve the domain name to its corresponding IP address. Resolvers cache the results of queries for a certain period (defined by the Time to Live or TTL value in the DNS record), which helps improve performance and reduce the load on the DNS system.