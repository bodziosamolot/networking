- In Mac i can't access docker's internal network by default. The container has access outside of the docker's internal network.
- In Linux i can access docker's internal network by default

- RUN - executes command at the time of building an image
- CMD - executes command at the time of running the container

- Docker containers can't talk to each other by name because they DNS service for them is the docker hosts DNS who does not know about the names.

- docker network create [name] --subnet 10.0.0.0/24
- docker newtowkr inspect [name]

- on the bridge network dns queries are forwarded to the machines dns which does not know about container names
- when i create a custom network, each container gets it's own local DNS server which knows the names of other containers
