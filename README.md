# D0RK3R

```
  ____  _____  ____  _  ____  _____  ____
 (  _ \(  _  )(  _ \( )/ ___)(  _  )(  _ \
  )(_) ))(_)(( )(_) )|\___ \ )(_)(( )___/
 (____/(_____)(____/(_)(____/(_____)(__)

 Author : https://github.com/infohlaingbwar
```

Shodan dork IP extractor. No API key needed. Supports proxy rotation.

---

## Install

```bash
git clone https://github.com/infohlaingbwar/d0rk3r
cd d0rk3r
pip install requests[socks]
python3 d0rk3r.py -q "port:443"
```

Auto-installs `requests` if missing.

### Termux

```bash
pkg install python
pip install requests[socks]
git clone https://github.com/infohlaingbwar/d0rk3r
cd d0rk3r
python d0rk3r.py -q "port:443"
```

### Kali / Debian / Ubuntu / WSL (PEP 668 error)

```bash
pip3 install --break-system-packages requests[socks]
python3 d0rk3r.py -q "port:443"
```

---

## Usage

### Basic (no proxy)

```
python3 d0rk3r.py -q "port:443 country:MM"
python3 d0rk3r.py -q "nginx"
python3 d0rk3r.py -q "port:80 os:Windows"
```

### With proxy file

Create `proxy.txt`:

```
http://user:pass@1.2.3.4:8080
socks5://5.6.7.8:1080
http://9.10.11.12:3128
```

Then:

```
python3 d0rk3r.py -q "port:443" -p proxy.txt --pages 5
```

### Save output

```
python3 d0rk3r.py -q "ActiveMQ" -p proxy.txt -o results.txt
```

---

## Flags

| Flag | Description |
|------|-------------|
| `-q` | Shodan dork query |
| `-p` | Path to proxy file |
| `--pages` | Requests per proxy (default: 2) |
| `--page-max` | Max total requests (0 = auto) |
| `-o` | Save output to file |
| `--timeout` | Request timeout in sec |
| `--delay` | Delay between requests in sec |
| `--no-banner` | Skip banner |

---

## How it bypasses Shodan free limit

Shodan free gives ~2 pages per IP.

With proxy rotation, each proxy has its own rate limit:

```
Proxy A → page 1 (~30 IPs)
Proxy B → page 1 (~30 new IPs)
Proxy C → page 1 (~30 new IPs)
...
```

10 proxies × 2 pages = 200-600+ unique IPs.

---

## Note

This scrapes Shodan's public web search. IP accuracy is not guaranteed. Always verify results yourself.
