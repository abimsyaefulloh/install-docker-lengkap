# install-docker-lengkap
Oke, Abim 😎 — kita bahas **cara install Docker lengkap di Ubuntu** (terbaru & clean).
Langkah-langkah ini bisa kamu ikuti di **Ubuntu Desktop, Server, WSL**, atau **VM di GCP**.

---

## 🧰 1. Update Sistem

Jalankan dulu:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 🧹 2. Hapus Versi Lama (kalau ada)

```bash
sudo apt remove docker docker-engine docker.io containerd runc
```

---

## 🧩 3. Install Dependensi

```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```

---

## 🔑 4. Tambahkan GPG Key Resmi Docker

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

---

## 📦 5. Tambahkan Repository Docker

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

---

## ⚙️ 6. Update lagi dan Install Docker Engine

```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

---

## 🧪 7. Tes Instalasi Docker

Coba jalankan:

```bash
sudo docker run hello-world
```

Kalau muncul pesan “Hello from Docker!”, berarti sudah sukses 🚀

---

## 👤 8. (Opsional tapi penting) Jalankan Docker tanpa `sudo`

Biar gak ribet ketik `sudo` terus:

```bash
sudo usermod -aG docker $USER
```

Lalu **logout & login lagi**, atau jalankan:

```bash
newgrp docker
```

Tes lagi:

```bash
docker ps
```

Kalau gak error = sukses 💪

---

## 🧩 9. (Opsional) Install Docker Compose versi lama (kalau butuh file `docker-compose.yml`)

Kalau kamu pakai `docker compose up` udah cukup, tapi kalau butuh versi standalone:

```bash
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" \
  -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

---

## 🧯 10. (Opsional) Pastikan Docker Start Otomatis

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

---

### ✅ Cek Versi

```bash
docker --version
docker compose version
```

---

Kamu mau sekalian aku bantu buat *cek script otomatis* (1 file `.sh`) biar tinggal `bash install-docker.sh` aja?
Bisa aku tulisin sekalian lengkap auto install + setup user.

