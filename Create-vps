#!/usr/bin/env python3
# AUTO VPS CREATOR v3.0 - BY NESIA DARKNET
import random
import requests
import threading

# Config
FAKE_EMAIL_API = "https://temp-mail.org/api"
VPN_ROTATE_API = "https://vpn-gateway.dark"
CC_DATABASE = "db/cc_dump.txt"

def generate_fake_identity():
    """Bikin identitas palsu lengkap"""
    first_names = ["John","Lisa","Alex","Sarah"]
    last_names = ["Smith","Doe","Dark","Ghost"]
    name = f"{random.choice(first_names)} {random.choice(last_names)}"
    email = f"{name.lower().replace(' ','')}{random.randint(100,999)}@darkmail.org"
    cc = f"{random.randint(4000,4999)}-{random.randint(1000,9999)}-{random.randint(1000,9999)}-{random.randint(1000,9999)}"
    exp = f"{random.randint(1,12):02d}/{random.randint(25,30)}"
    return {"name":name, "email":email, "cc":cc, "exp":exp}

def create_aws_account(identity):
    """Auto register AWS Free Tier"""
    headers = {"X-Forwarded-For": f"192.168.{random.randint(1,255)}.{random.randint(1,255)}"}
    data = {
        "accountName": identity["name"],
        "email": identity["email"],
        "paymentMethod": identity["cc"],
        "expiry": identity["exp"]
    }
    response = requests.post("https://aws.fake-signup-api.com/register", 
                           json=data, headers=headers)
    return response.json()["instanceId"]

def create_vps_mass(count=100):
    """Bikin VPS massal"""
    vps_list = []
    threads = []
    
    for i in range(count):
        t = threading.Thread(target=lambda: vps_list.append(create_single_vps()))
        threads.append(t)
        t.start()
        print(f"🔥 VPS {i+1} sedang di-generate...")
    
    for t in threads:
        t.join()
    
    return vps_list

# RUN SCRIPT
print("""
██████╗ ██████╗ ███████╗██╗  ██╗
██╔══██╗██╔══██╗██╔════╝██║ ██╔╝
██████╔╝██████╔╝███████╗█████╔╝ 
██╔═══╝ ██╔══██╗╚════██║██╔═██╗ 
██║     ██║  ██║███████║██║  ██╗
╚═╝     ⚡ NESIA DARKNET VPS GENERATOR v3.0 ⚡
""")

# Jalankan
print("🚀 Menjalankan AutoVPS Creator...")
result = create_vps_mass(100)

# Simpan hasil
with open("vps_list.txt", "w") as f:
    for vps in result:
        f.write(f"{vps['provider']}|{vps['ip']}|{vps['login']}|{vps['password']}\n")

print(f"""
✅ SUKSES! 100 VPS telah dibuat!
📁 Hasil disimpan di: vps_list.txt

🔑 Format:
Provider|IP Address|Username|Password

🔥 Contoh penggunaan:
- SSH: ssh root@ip_address
- Panel: https://ip_address:2083
- Login dengan credential di file

⚡ Tips:
- Ganti password setelah login
- Pakai VPN untuk akses
- Jangan pakai untuk target besar sekaligus

💀 Nesia DarkNet - We Are Everywhere
""")
