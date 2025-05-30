## Secured and Monitored Web Infrastructure Diagram (ASCII)

````
                       +-------------------+
                       |   Internet Users  |
                       +-------------------+
                                │
                                ▼
                       +-------------------+
                       |   Firewall 1      |
                       +-------------------+
                                │
                                ▼
                       +-------------------+
                       |  Load Balancer    |  (SSL/HTTPS)
                       +-------------------+
                                │
         +----------------------+----------------------+
         |                      |                      |
   +-------------+       +-------------+        +-------------+
   | Firewall 2  |       | Firewall 2  |        | Firewall 2  |
   +-------------+       +-------------+        +-------------+
         │                      │                      │
         ▼                      ▼                      ▼
   +-------------+       +-------------+        +-------------+
   | Web Server 1|       | Web Server 2|        | Web Server 3|
   | + App Layer |       | + App Layer |        | + App Layer |
   | + Monitoring|       | + Monitoring|        | + Monitoring|
   +------+------+       +------+------+        +------+------+
         |                      |                      |
         +----------+-----------+----------------------+
                    |
            +-------------------+
            |  MySQL Database   |  (Single write-enabled DB)
            +-------------------+
                    |
            +-------------------+
            |   Firewall 3      |
            +-------------------+
````

Legend:
- **Firewall 1:** Protects the load balancer from the public.
- **Firewall 2 (x3):** Protects each web/app server.
- **Firewall 3:** Protects the database.
- **Load Balancer:** Terminates SSL, distributes HTTPS traffic.
- **Web/App Servers:** Serve web/app content, run monitoring agents.
- **MySQL Database:** Stores persistent data.

---

## 2. Secured and Monitored Web Infrastructure

### What I changed
Added security and monitoring to the distributed setup.

### My setup
- **1 Load Balancer:** Handles HTTPS, terminates SSL.
- **3 Firewalls:** One before LB, one before each web/app server, one before DB.
- **3 Web/App Servers:** Each runs web server, app layer, and monitoring agent.
- **1 MySQL Database:** Single write-enabled DB, protected by a firewall.
- **Monitoring:** Agents on each web/app server.

### Why I added this
- **Firewalls:** Restrict access and protect each layer.
- **SSL:** Encrypts user traffic for security.
- **Monitoring:** Tracks server health and performance.

### How it works
1. User connects via HTTPS to the load balancer.
2. Firewall 1 restricts public access to the LB.
3. LB distributes traffic to web/app servers, each protected by Firewall 2.
4. Web/app servers process requests, monitored by agents.
5. All connect to a single MySQL DB, protected by Firewall 3.

### Limitations / Risks
- **SSL Termination at LB:** Traffic between LB and web servers is unencrypted unless re-encrypted.
- **Single DB:** Single point of failure, no horizontal scalability.
- **All-in-one servers:** Hard to scale independently, failure in one component can affect others.
- **Improvements:** Use end-to-end encryption, DB replication, and separate web/app/monitoring roles.

