# D0RK3R

```
  ____  _____  ____  _  ____  _____  ____
 (  _ \(  _  )(  _ \( )/ ___)(  _  )(  _ \
  )(_) ))(_)(( )(_) )|\___ \ )(_)(( )___/
 (____/(_____)(____/(_)(____/(_____)(__)

 Author : https://github.com/infohlaingbwar
```

Shodan မှာ dork ရိုက်ပြီး IP တွေဆွဲထုတ်ဖို့သုံးတာ။ API key မလိုဘူး။ Proxy ထည့်သုံးလို့ရတယ်။

---

##Installလုပ်ရန်

```bash
git clone https://github.com/infohlaingbwar/d0rk3r
cd d0rk3r
pip install requests[socks]
python3 d0rk3r.py -q "port:443"
```

မရှိရင် ကိုယ့်ဘာသာ install လုပ်စရာမလိုဘူး — tool က run တာနဲ့ auto install လုပ်ပေးတယ်။

### Termux

```bash
pkg install python
pip install requests[socks]
git clone https://github.com/infohlaingbwar/d0rk3r
cd d0rk3r
python d0rk3r.py -q "port:443"
```

### Kali / Debian / Ubuntu / WSL (PEP 668 error ရင်)

```bash
pip3 install --break-system-packages requests[socks]
python3 d0rk3r.py -q "port:443"
```

---

## သုံးနည်း

### ရိုးရိုး (proxy မပါ)

```
python3 d0rk3r.py -q "port:443 country:MM"
python3 d0rk3r.py -q "nginx"
python3 d0rk3r.py -q "port:80 os:Windows"
```

### proxy ပါ

proxy.txt ထဲမှာ ဒီလိုရေး

```
http://user:pass@1.2.3.4:8080
socks5://5.6.7.8:1080
http://9.10.11.12:3128
```

ပြီးရင်

```
python3 d0rk3r.py -q "port:443" -p proxy.txt --pages 5
```

### result သိမ်း

```
python3 d0rk3r.py -q "ActiveMQ" -p proxy.txt -o results.txt
```

---

## Flag တွေ

| Flag | ရှင်းလင်းချက် |
|------|----------------|
| `-q` | dork query |
| `-p` | proxy.txt လမ်းကြောင်း |
| `--pages` | proxy တစ်လုံးစီအတွက် request အရေအတွက် (default 2) |
| `--page-max` | total request အများဆုံး |
| `-o` | output သိမ်းမယ် |
| `--timeout` | request timeout |
| `--delay` | တစ်ခါပြီးတိုင်းစောင့်မယ် |
| `--no-banner` | banner မပြစေချင်ရင် |

---

## Shodan free limit ကို ဘယ်လိုကျော်လဲ

Shodan free က IP တစ်ခုကို ၂ page လောက်ပဲပေးတယ်။

Proxy သုံးရင် proxy တစ်လုံးချင်းစီမှာ သူ့ limit သူရှိတယ်။ ဒါကို လှည့်သုံးလိုက်တာ။

Proxy A → page 1 (IP 30)
Proxy B → page 1 (အသစ် 30)
Proxy C → page 1 (အသစ် 30)

Proxy 10 လုံး × 2 pages ဆို IP 200-600+ ရနိုင်တယ်။

---



Shodan web search ကို scrape လုပ်တာဖြစ်လို့ IP တွေက တိကျချင်မှတိကျမယ်။ ရလာတဲ့ IP တွေကို ကိုယ်တိုင်ပြန်စစ်ဖို့လိုတယ်။
