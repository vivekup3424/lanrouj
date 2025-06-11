---
tags:
  - mongodb
  - database
---

## 🧠 **What is `mongod`?**

### **Definition**
- `mongod` is the **primary daemon process** for MongoDB. It **runs the MongoDB database server**.
- It handles **data storage**, **query processing**, **replication**, **authentication**, **indexing**, and **server configuration**.

### **Mnemonic**
Think of `mongod` as:
> **"Mongo Daemon"** – the main background service that stores and serves your data.

---

## 🧰 **Core Responsibilities of `mongod`**

| Feature | Description |
|--------|-------------|
| **Data Storage** | Stores documents and indexes on disk using a storage engine (WiredTiger by default). |
| **Query Processing** | Parses and executes client queries (CRUD operations). |
| **Networking** | Listens for connections (default port: 27017). |
| **Indexing** | Builds and maintains B-tree indexes for efficient lookups. |
| **Replication** | Supports replication via **oplog.rs** in a replica set. |
| **Write-Ahead Logging (Journaling)** | Ensures crash-safe durability with commit logs. |
| **Authentication & Authorization** | Supports role-based access control. |
| **Monitoring & Metrics** | Exposes internal metrics for logging and profiling. |

---

## 🧱 **Startup Behavior**

### **Starting `mongod`**

There are three ways to start `mongod`:

#### 1. **Default Startup**
```bash
mongod
```
- Starts with default data directory (`/data/db`).
- Listens on port `27017`.

#### 2. **With Config File**
```bash
mongod --config /etc/mongod.conf
```
- Configuration driven startup (YAML file).
- Preferred in production.

#### 3. **With Command Line Options**
```bash
mongod --dbpath /custom/db --port 28017 --auth --replSet rs0
```

---

## ⚙️ **Key Configuration Parameters**

| Parameter | Purpose |
|----------|---------|
| `--dbpath` | Path to the database files. Default: `/data/db` |
| `--port` | Port to listen for client connections. Default: `27017` |
| `--bind_ip` | IP addresses to listen on (e.g., `127.0.0.1,192.168.1.10`) |
| `--logpath` | Path to log file |
| `--fork` | Run as a daemon (background) process |
| `--auth` | Enable authentication |
| `--replSet` | Initialize or join a replica set |
| `--shardsvr` | Marks the `mongod` as a shard member |
| `--config` | Path to a YAML/INI-style configuration file |

---

## 🧠 **Memory and Storage Internals**

### **1. Storage Engine**
- Default: **WiredTiger**
- Others (deprecated/optional): MMAPv1, In-Memory

### **2. Journaling**
- All writes go to a journal before being committed.
- Ensures **crash recovery**.

### **3. Write Concern**
- Controls write acknowledgment:
  - `w: 1` (ack from primary)
  - `w: majority` (ack from most nodes)

### **4. Cache Management**
- WiredTiger uses ~50% of available RAM by default.
- Uses OS-level memory-mapped files.

---

## 🔁 **Replication and `mongod`**

In a **replica set**, each node runs a `mongod` process.

### Replica Set Members:
| Role | Description |
|------|-------------|
| **Primary** | Handles all writes, replicates to secondaries |
| **Secondary** | Pulls changes from primary via `oplog.rs` |
| **Arbiter** | Votes in elections but doesn’t hold data |

### Replication Flow:
```text
Client → Primary (write)
        Primary → oplog.rs → Secondary nodes (pull oplog)
```

---

## 🔒 **Security**

### **Authentication**
- Enabled using `--auth`.
- User-based authentication with roles (read, readWrite, dbAdmin, etc.)

### **Authorization**
- Roles define what actions a user can perform.

### **TLS/SSL**
- `mongod` supports encrypted connections via certificates.

---

## 📈 **Monitoring and Performance**

### Tools
- **`mongotop`**: Live read/write activity per collection
- **`mongostat`**: Server metrics (ops/sec, mem, net)
- **Profiler**: Records slow or expensive queries

### Logs
- Stored at the path specified by `--logpath`
- Includes startup status, slow queries, warnings

---

## 🧪 **Testing and Debugging**

### Useful flags:
| Flag | Purpose |
|------|---------|
| `--verbose` | Verbose logging |
| `--profile` | Enable database operation profiler |
| `--repair` | Attempt to fix corrupted database files |
| `--nojournal` | Disable journaling (not safe for production) |

---

## 🧩 **Differences Between `mongod`, `mongo`, and `mongos`**

| Component | Purpose |
|----------|---------|
| `mongod` | The **core server** that runs the MongoDB database |
| `mongo` | The **shell client** used to connect and interact with `mongod` |
| `mongos` | The **router process** in a sharded MongoDB cluster |

---

## 📌 **Sample `mongod.conf` File**

```yaml
systemLog:
  destination: file
  path: "/var/log/mongodb/mongod.log"
  logAppend: true

storage:
  dbPath: "/var/lib/mongo"
  journal:
    enabled: true

net:
  port: 27017
  bindIp: 127.0.0.1

security:
  authorization: enabled

replication:
  replSetName: "rs0"
```

---

## 📚 Summary Cheatsheet

| Feature | Summary |
|--------|---------|
| **Process** | Background server that handles all DB ops |
| **Port** | Default is 27017 |
| **Data Dir** | Default is `/data/db` |
| **Storage Engine** | WiredTiger |
| **Replication** | Handled with oplog and replica sets |
| **Security** | Role-based access, optional TLS |
| **Startup** | CLI or config file |
| **Logs** | Help in debugging performance and issues |

---

Let me know if you want a **PDF version**, **diagram of internal architecture**, or dive into any specific topic like **oplog.rs**, **failover process**, or **how WiredTiger works**.