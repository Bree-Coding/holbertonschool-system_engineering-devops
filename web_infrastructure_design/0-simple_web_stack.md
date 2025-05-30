## Simple Web Stack Diagram (ASCII)

````
                       +-------------------+
                       |      User         |
                       +-------------------+
                                │
                                ▼
                       +-------------------+
                       |   DNS Server      |
                       +-------------------+
                                │
                                ▼
                       +-------------------+
                       |   Web Server      |
                       |     (Nginx)       |
                       +-------------------+
                                │
                                ▼
                       +-------------------+
                       | Application Server|
                       +-------------------+
                                │
                                ▼
                       +-------------------+
                       | Application Files |
                       +-------------------+
                                │
                                ▼
                       +-------------------+
                       |  MySQL Database   |
                       +-------------------+
````

Legend:
- **DNS Server:** Resolves `www.foobar.com` to the server's IP.
- **Web Server (Nginx):** Handles HTTP requests, serves static files, forwards dynamic requests.
- **Application Server:** Runs backend logic.
- **Application Files:** The codebase for the application.
- **MySQL Database:** Stores persistent data.

---

## 0. Simple Web Stack

### What I changed
This is the most basic setup: a single server running all components.

### My setup
- **1 Server:** Runs Nginx, application server, application files, and MySQL database.
- **DNS:** Points `www.foobar.com` to the server's IP.

### Why I used this
- **Simplicity:** Easy to set up and manage for small projects or prototypes.
- **Cost:** Only one server needed.

### How it works
1. User enters `www.foobar.com` in the browser.
2. DNS resolves the domain to the server's IP.
3. The browser sends an HTTP request to the server.
4. Nginx handles the request, serves static files or forwards to the application server.
5. The application server processes logic, accesses the database if needed, and returns a response.

### Limitations
- **Single Point of Failure:** If the server goes down, the whole site is offline.
- **No scalability:** Can't handle high traffic.
- **No security:** No HTTPS or firewall.
- **No monitoring:** Issues are only found by manual checking.
