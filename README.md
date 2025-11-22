# opencti-writeup
My experience using OpenCTI for threat intel
<img width="1908" height="932" alt="image" src="https://github.com/user-attachments/assets/20300d1d-471b-46a7-a7d4-fe8768a17dff" />
# OpenCTI Deployment using Docker & Docker Compose  
### تشغيل ونشر منصة OpenCTI باستخدام Docker على Ubuntu

---



## 📌 مقدمة  
هذا المشروع يحتوي على تهيئة كاملة لتشغيل منصة **OpenCTI** باستخدام Docker و Docker Compose، مع ضبط جميع التبعيات مثل Elasticsearch و Redis و MinIO و RabbitMQ بالإضافة إلى مجموعة من الـ Connectors الجاهزة.

تم إعداد هذا التوثيق لشرح خطوات التثبيت، التجهيز، التشغيل، والتحقق بشكل كامل.

---

## 📁 هيكل المشروع
```
.
└── nawafOpecti
    └── docker
        ├── docker-compose.yml
        ├── docker-compose.dev.yml
        ├── rabbitmq.conf
        ├── README.md
        └── renovate.json
```

---

## ⚙️ متطلبات التشغيل
- نظام Linux (يفضّل Ubuntu 22.04 أو 24.04)
- Docker Engine
- Docker Compose Plugin
- ذاكرة RAM لا تقل عن 8GB

---

## 🐳 تثبيت Docker على Ubuntu
```bash
sudo apt update
sudo apt upgrade -y
sudo apt install ca-certificates curl gnupg -y

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
```

---

## 🧪 التحقق من تثبيت Docker
```bash
docker info
docker ps
```

---

## 📄 ملف البيئة `.env`
> ⚠️ تمت إزالة التوكنات الحقيقية واستبدالها بقيم آمنة

```
OPENCTI_ADMIN_EMAIL=admin@opencti.io
OPENCTI_ADMIN_PASSWORD=<REPLACE_ME>
OPENCTI_ADMIN_TOKEN=<REPLACE_ME>
OPENCTI_BASE_URL=http://localhost:8080
OPENCTI_HEALTHCHECK_ACCESS_KEY=<REPLACE_ME>

MINIO_ROOT_USER=<REPLACE_ME>
MINIO_ROOT_PASSWORD=<REPLACE_ME>

RABBITMQ_DEFAULT_USER=guest
RABBITMQ_DEFAULT_PASS=guest

ELASTIC_MEMORY_SIZE=4G

CONNECTOR_HISTORY_ID=<REPLACE_ME>
CONNECTOR_EXPORT_FILE_STIX_ID=<REPLACE_ME>
CONNECTOR_EXPORT_FILE_CSV_ID=<REPLACE_ME>
CONNECTOR_IMPORT_FILE_STIX_ID=<REPLACE_ME>

SMTP_HOSTNAME=localhost
```

---

## 🚀 تشغيل OpenCTI
انتقل لمجلد المشروع:

```bash
cd nawafOpecti/docker
docker compose up -d
```

---

## 🔍 التحقق من تشغيل الخدمات
```bash
docker compose ps
```

---

## 🌐 الدخول إلى OpenCTI
بعد أن تصبح كل الخدمات **healthy**:

```
http://<YOUR-SERVER-IP>:8080
```

مثال:

```
http://192.158.200.88:8080
```

### بيانات الدخول:
- Email: `admin@opencti.io`
- Password: التي وضعتها في `.env`

---

---



## 📜 Changelog
- Added full OpenCTI Docker deployment  
- Removed all sensitive secrets/tokens for security  
- Includes documentation in Arabic & English  

---

# 🎉 Done!  
 

