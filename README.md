# D0RK3R

```
  ____  _____  ____  _  ____  _____  ____
 (  _ \(  _  )(  _ \( )/ ___)(  _  )(  _ \
  )(_) ))(_)(( )(_) )|\___ \ )(_)(( )___/
 (____/(_____)(____/(_)(____/(_____)(__)

 Author : https://github.com/infohlaingbwar
```

Shodan dork IP extractor with **auto-proxy** support. No API key needed.

---

## Features

✅ **Auto-proxy** — Fetch working proxies from GitHub automatically  
✅ **Proxy rotation** — Bypass Shodan rate limits  
✅ **Smart caching** — Reuse proxies for 6 hours  
✅ **No API key** — Scrapes public Shodan search  
✅ **Fast extraction** — Get 100s-1000s of IPs in seconds  

---

## Install

```bash
git clone https://github.com/infohlaingbwar/d0rk3r
cd d0rk3r
pip install requests[socks]
python3 d0rk3r.py -q "port:443" --auto-proxy
```

Auto-installs `requests` if missing.

### Termux

```bash
pkg install python
pip install requests[socks]
git clone https://github.com/infohlaingbwar/d0rk3r
cd d0rk3r
python d0rk3r.py -q "port:443" --auto-proxy
```

### Kali / Debian / Ubuntu / WSL (PEP 668 error)

```bash
pip3 install --break-system-packages requests[socks]
python3 d0rk3r.py -q "port:443" --auto-proxy
```

---

## Usage

### Auto-proxy (recommended)

```bash
# CVE hunting
python3 d0rk3r.py -q "Apache/2.4.49" --auto-proxy -o results.txt

# Bug bounty recon
python3 d0rk3r.py -q 'org:"Tesla Motors"' --auto-proxy --pages 3

# IoT devices
python3 d0rk3r.py -q "port:554 rtsp country:MM" --auto-proxy

# Vulnerable hosts
python3 d0rk3r.py -q "vuln:CVE-2021-41773" --auto-proxy
```

### Manual proxy file

Create `proxy.txt`:

```
http://user:pass@1.2.3.4:8080
socks5://5.6.7.8:1080
http://9.10.11.12:3128
```

Then:

```bash
python3 d0rk3r.py -q "port:443" -p proxy.txt --pages 5
```

### No proxy (direct)

```bash
python3 d0rk3r.py -q "nginx country:MM"
```

---

## Shodan Dork Syntax

| Syntax | Example | Description |
|--------|---------|-------------|
| `port:` | `port:22` | SSH open hosts |
| `country:` | `country:MM` | Myanmar servers |
| `city:` | `city:Yangon` | City location |
| `org:` | `org:"MPT"` | Organization |
| `hostname:` | `hostname:gov.mm` | Domain names |
| `os:` | `os:Windows` | Operating system |
| `product:` | `product:nginx` | Software |
| `vuln:` | `vuln:CVE-2021-41773` | CVE vulnerable |
| `http.title:` | `http.title:"admin"` | Page titles |
| `ssl:` | `ssl:"Myanmar"` | SSL cert info |

**Combine queries:**

```bash
python3 d0rk3r.py -q "Apache/2.4.49 country:MM port:443" --auto-proxy
```

---

## Flags

| Flag | Description |
|------|-------------|
| `-q` | Shodan dork query (required) |
| `--auto-proxy` | Auto-fetch proxies from GitHub |
| `-p` | Path to manual proxy file |
| `--pages` | Requests per proxy (default: 2) |
| `--page-max` | Max total requests (0 = auto) |
| `-o` | Save output to file |
| `--timeout` | Request timeout in sec (default: 10) |
| `--delay` | Delay between requests in sec (default: 0.5) |
| `--no-banner` | Skip banner |

---

## How It Works

### Auto-Proxy

1. Fetches fresh proxies from GitHub public lists
2. Verifies working proxies (tests sample of 100)
3. Caches proxies for 6 hours
4. Rotates proxies during scraping

### Shodan Bypass

Shodan free gives ~2 pages per IP.

With proxy rotation:

```
Proxy A → page 1 (~300 IPs)
Proxy B → page 1 (~300 new IPs)
Proxy C → page 1 (~300 new IPs)
...
```

10 proxies × 2 pages = 600-3000+ unique IPs.

---

## Example Output

```bash
$ python3 d0rk3r.py -q "nginx" --auto-proxy --pages 1

 [*] Auto-fetching proxies...
 [+] Loaded 13 working proxies
 ┌─ Proxies   : 13
 ├─ Requests  : 13 (1 per proxy)
 └─ Query     : nginx

 ════════════════════════════════════════════════
 ✔ 1005 unique IPs  │ 1 req OK  │ 12 fail  │ 55.0s
 ════════════════════════════════════════════════
 ├─ 101.230.14.203
 ├─ 102.182.100.18
 ├─ 103.100.84.76
 ...
 └─ 1005 total
```

---

## Files

| File | Purpose |
|------|---------|
| `d0rk3r.py` | Main script |
| `proxy_fetcher.py` | Auto-proxy module |
| `.proxy_cache.txt` | Cached proxies (auto-generated) |

---

## Note

This scrapes Shodan's public web search. IP accuracy is not guaranteed. Always verify results yourself.

For educational and authorized testing only.

---

## License

MIT
