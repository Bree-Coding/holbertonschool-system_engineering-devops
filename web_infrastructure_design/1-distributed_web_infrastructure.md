## Distributed Web Infrastructure Diagram (ASCII)

````
                       +-------------------+
                       |      User         |
                       +-------------------+
                                │
                                ▼
                     +-----------------------+
                     |     Load Balancer     | ← HAProxy (Round Robin)
                     +-----------------------+
                          │             │
                          ▼             ▼
               +----------------+   +----------------+
               |   Web Server 1 |   |   Web Server 2 |
               |     (Nginx)    |   |     (Nginx)    |
               +----------------+   +----------------+
                        │                   │
                        ▼                   ▼
              +-------------------+ +-------------------+
              | App Server 1      | | App Server 2      |
              | (App Code files)  | | (App Code files)  |
              +-------------------+ +-------------------+
                        │                   │
                        ▼                   ▼
              +-------------------+ +-------------------+
              | MySQL DB (Primary)| | MySQL DB (Replica)|
              +-------------------+ +-------------------+
````

Legend:
- Load Balancer: Distributes traffic using **Round Robin**.
- Web Servers: Handle incoming HTTP requests.
- App Servers: Run backend logic and interact with the DB.
- MySQL DB: Primary node handles writes; replica node handles reads.


## 1. Distributed Web Infrastructure

### What I changed
To improve the first setup, I added more servers and a load balancer.

### My new setup
- **1 Load Balancer (HAProxy):** Sends users to different backend servers.
- **2 Backend servers** (same config on both):
  - Nginx
  - Application server
  - Application code
  - MySQL database

### Why I added this
- **Load balancer:** Shares traffic between servers so one isn't overloaded.
- **2 servers:** Redundancy and better performance if there are many users.
 
### Load balancing
- I used the **Round Robin** algorithm, which sends users one by one to each server in turn.

### Active-Active mode
Both servers work at the same time. If one fails, the other still works.

### Database setup: Primary-Replica
- **Primary server:** Handles writes.
- **Replica server:** Only reads, and copies data from the primary.
- **App behavior:** It writes to the primary, reads from both.

### Weak points
- **SPOF:** If the load balancer fails, nobody can access the site.
- **No security:** No HTTPS or firewall yet.
- **No monitoring:** I can’t know if something is wrong unless I check manually.
