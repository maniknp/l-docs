### Using `netstat`

`netstat` is a network statistics utility that can display various network connections and related information.

**Installation:**
- On many Linux distributions, `netstat` is part of the `net-tools` package. Install it using:
  ```sh
  sudo apt-get install net-tools   # Debian/Ubuntu
  sudo yum install net-tools       # CentOS/RHEL
  ```

**Usage:**

1. **List All Active Connections:**
   ```sh
   netstat -an
   ```

2. **Filter for TCP Connections:**
   ```sh
   netstat -ant
   ```

3. **Filter for UDP Connections:**
   ```sh
   netstat -anu
   ```

4. **List Active Connections to a Specific Port (e.g., port 80 for HTTP):**
   ```sh
   netstat -an | grep :80
   ```

5. **List Active Connections with Process Information:**
   ```sh
   sudo netstat -tulnp
   ```

**Example:**
```
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      1234/nginx: master
tcp        0      0 192.168.1.100:80        192.168.1.101:56789     ESTABLISHED 1234/nginx: worker
tcp        0      0 192.168.1.100:80        192.168.1.102:56790     ESTABLISHED 1234/nginx: worker
```

### Using `ss`

`ss` (socket statistics) is a modern replacement for `netstat` that provides more detailed information and faster results.

**Installation:**
- `ss` is typically included by default in the `iproute2` package on modern Linux distributions.

**Usage:**

1. **List All Active Connections:**
   ```sh
   ss -a
   ```

2. **Filter for TCP Connections:**
   ```sh
   ss -t
   ```

3. **Filter for UDP Connections:**
   ```sh
   ss -u
   ```

4. **List Active Connections to a Specific Port (e.g., port 80 for HTTP):**
   ```sh
   ss -at '( dport = :80 or sport = :80 )'
   ```

5. **List Active Connections with Process Information:**
   ```sh
   sudo ss -tulnp
   ```

**Example:**
```
Netid State      Recv-Q Send-Q Local Address:Port               Peer Address:Port              
tcp   LISTEN     0      128    0.0.0.0:80                      0.0.0.0:*                  
tcp   ESTAB      0      0      192.168.1.100:80                192.168.1.101:56789        
tcp   ESTAB      0      0      192.168.1.100:80                192.168.1.102:56790        
```

### Monitoring Specific Metrics

1. **Total Active Connections:**
   - Count the number of `ESTABLISHED` connections to get the total number of active connections.

2. **Connections per IP Address:**
   - Identify which IP addresses have the most connections, useful for detecting unusual activity or traffic patterns.

3. **Connection States:**
   - Monitor different states such as `LISTEN`, `ESTABLISHED`, `TIME_WAIT`, etc., to understand the connection lifecycle.

### Example Workflow to Monitor Nginx Connections

1. **Using `netstat` to Monitor Active Connections:**
   ```sh
   sudo netstat -ant | grep ':80' | grep 'ESTABLISHED'
   ```

2. **Using `ss` to Monitor Active Connections:**
   ```sh
   sudo ss -at '( dport = :80 or sport = :80 )' | grep 'ESTAB'
   ```

### Summary

- **`netstat`** provides a classic, straightforward way to view network connections and associated processes.
- **`ss`** is a faster, more detailed modern tool that can replace `netstat`.

