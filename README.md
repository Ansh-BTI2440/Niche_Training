# Niche_Training

## Create Two Ubuntu WSL Instances and Test Network Connectivity

### 1. Check Available WSL Distributions

Open **Command Prompt** or **PowerShell** and run:

`wsl -l -v`

Example output:

```text id="iyw5on"
  NAME              STATE           VERSION
* Ubuntu-24.04      Stopped         2
  ubuntu1           Stopped         2
  ubuntu2           Stopped         2
  docker-desktop    Running         2
```

---

### 2. Start the First Ubuntu Instance

Open the first terminal and run:

`wsl -d ubuntu1`

Inside `ubuntu1`, check the IP address:

`hostname -I`

Alternatively:

`ip addr show`

Save the IP address for later.

Example: `172.x.x.x`

---

### 3. Start the Second Ubuntu Instance

Open another **Command Prompt** or **PowerShell** window and run:

`wsl -d ubuntu2`

Inside `ubuntu2`, check its IP address:

`hostname -I`

Save this IP address as well.

---

### 4. Install the Ping Utility

Inside both Ubuntu instances, run:

`sudo apt update`

`sudo apt install -y iputils-ping`

---

### 5. Ping `ubuntu2` from `ubuntu1`

Inside the `ubuntu1` terminal, run:

`ping <UBUNTU2_IP_ADDRESS>`

Example:

`ping 172.x.x.x`

A successful connection should produce output similar to:

```text id="g9j6bi"
64 bytes from 172.x.x.x: icmp_seq=1 ttl=64 time=0.xxx ms
64 bytes from 172.x.x.x: icmp_seq=2 ttl=64 time=0.xxx ms
64 bytes from 172.x.x.x: icmp_seq=3 ttl=64 time=0.xxx ms
```

Stop the ping command using `Ctrl + C`.

---

### 6. Ping `ubuntu1` from `ubuntu2`

Inside the `ubuntu2` terminal, run:

`ping <UBUNTU1_IP_ADDRESS>`

Example:

`ping 172.x.x.x`

If the ping is successful, communication between the two WSL Ubuntu instances has been established.

---

### 7. Check Running WSL Instances

From Windows Command Prompt or PowerShell:

`wsl -l -v`

---

### 8. Stop a Specific WSL Instance

To stop `ubuntu1`:

`wsl --terminate ubuntu1`

To stop `ubuntu2`:

`wsl --terminate ubuntu2`

---

### 9. Stop All WSL Instances

`wsl --shutdown`

---

### 10. Delete a WSL Distribution

> **Warning:** This permanently deletes the distribution and all data inside it.

To delete `ubuntu1`:

`wsl --unregister ubuntu1`

To delete `ubuntu2`:

`wsl --unregister ubuntu2`

---

## Network Architecture

```text id="knquvf"
+-------------------+                 +-------------------+
|     ubuntu1       |                 |     ubuntu2       |
|                   |                 |                   |
|   hostname -I     |                 |   hostname -I     |
|        |          |                 |        |          |
|    IP Address     | ---- PING ----> |    IP Address     |
|                   | <--- PING ----- |                   |
+-------------------+                 +-------------------+
```

---

## Conclusion

Two Ubuntu WSL instances, `ubuntu1` and `ubuntu2`, were started successfully. Their IP addresses were identified using `hostname -I`, and network connectivity was tested using the `ping` command. Successful ping responses confirmed communication between the two Ubuntu WSL environments.
