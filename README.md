# superdjtechnic
# Sistem de Bonificații pentru Tehnicieni

Un sistem complet de management al bonificațiilor pentru echipa tehnică, cu KPI-uri automatizate, grafice de evoluție și funcționalități de export.

## 🚀 Funcționalități

### ✅ Sistem KPI
- **6 KPI-uri**: punctualitate, montare, erori, feedback, întreținere, vocabular
- **Scară punctaj**: 1-100 puncte pentru fiecare KPI
- **Calcul automat** al scorului final (media tuturor KPI-urilor)

### ✅ Sistem de Bonusare
- **≥ 90 puncte**: Bonus Mare (500 lei)
- **80-89 puncte**: Bonus Mediu (250 lei)
- **< 80 puncte**: Fără Bonus (0 lei)

### ✅ Dashboard & Statistici
- Statistici în timp real
- Performanța echipei
- Total bonusuri acordate
- Evaluări lunare

### ✅ Grafice de Evoluție
- **Evoluție individuală** pentru fiecare tehnician
- **Analiza echipei** pe luni
- **Tendințe KPI** în timp
- **Evoluția bonusurilor**

### ✅ Export de Date
- **Export Excel** (.xlsx) cu toate datele
- **Export PDF** profesional cu rapoarte
- Date complete: KPI-uri, scoruri, bonusuri, istorice

### ✅ Management Tehnicieni
- Adăugare tehnicieni noi
- Istoric complet evaluări
- Profile individuale

## 🔧 Tehnologii

### Backend
- **FastAPI** - API modern și rapid
- **MongoDB** - Baza de date NoSQL
- **Pydantic** - Validare și serializare date
- **ReportLab** - Generare PDF-uri
- **Motor** - Driver async pentru MongoDB

### Frontend
- **React** - Interfață utilizator moderna
- **Tailwind CSS** - Styling rapid și responsive
- **Recharts** - Grafice interactive
- **Axios** - Client HTTP
- **XLSX** - Export Excel

## 📦 Instalare și Configurare

### 1. Cerințe de Sistem
- **Python 3.11+**
- **Node.js 18+**
- **MongoDB 5.0+**
- **Yarn** (package manager pentru frontend)

### 2. Instalare Backend

bash
# Navigează în directorul backend
cd backend

# Creează mediu virtual Python
python -m venv venv
source venv/bin/activate  # Linux/Mac
# sau
venv\Scripts\activate     # Windows

# Instalează dependențele
pip install -r requirements.txt

# Configurează variabilele de mediu
cp .env.example .env
# Editează .env cu setările tale:
# MONGO_URL="mongodb://localhost:27017"
# DB_NAME="bonus_system"


### 3. Instalare Frontend

bash
# Navigează în directorul frontend
cd frontend

# Instalează dependențele
yarn install

# Configurează variabilele de mediu
cp .env.example .env
# Editează .env cu URL-ul backend-ului:
# REACT_APP_BACKEND_URL=http://localhost:8001


### 4. Pornire MongoDB

bash
# Pornește MongoDB local
mongod

# Sau folosește Docker
docker run -d -p 27017:27017 --name mongodb mongo:latest


## 🚀 Rulare Aplicație

### 1. Pornește Backend-ul

bash
cd backend
source venv/bin/activate
uvicorn server:app --host 0.0.0.0 --port 8001 --reload


Backend-ul va fi disponibil la: http://localhost:8001
API Documentation: http://localhost:8001/docs

### 2. Pornește Frontend-ul

bash
cd frontend
yarn start


Frontend-ul va fi disponibil la: http://localhost:3000

## 📁 Structura Proiectului

/
├── backend/                 # API FastAPI
│   ├── server.py           # Aplicația principală
│   ├── requirements.txt    # Dependențe Python
│   └── .env               # Variabile de mediu
├── frontend/               # Aplicația React
│   ├── src/
│   │   ├── App.js         # Componenta principală
│   │   ├── App.css        # Stiluri CSS
│   │   ├── index.js       # Punct de intrare
│   │   └── index.css      # Stiluri globale
│   ├── package.json       # Dependențe Node.js
│   ├── tailwind.config.js # Configurare Tailwind
│   └── .env              # Variabile de mediu frontend
└── README.md              # Documentația proiectului


## 🔄 API Endpoints

### Tehnicieni
- GET /api/technicians - Listează toți tehnicienii
- POST /api/technicians - Creează tehnician nou
- GET /api/technicians/{id} - Detalii tehnician specific

### Evaluări
- GET /api/evaluations - Listează toate evaluările
- POST /api/evaluations - Creează evaluare nouă
- GET /api/evaluations/technician/{name} - Evaluări pentru un tehnician

### Analytics
- GET /api/dashboard/stats - Statistici dashboard
- GET /api/analytics/technician-evolution/{name} - Evoluția unui tehnician
- GET /api/analytics/team-performance - Performanța echipei

### Export
- GET /api/export/pdf - Export PDF cu toate evaluările

## 🎯 Utilizare

### 1. Adăugare Tehnicieni
1. Mergi la tab-ul "Gestionare"
2. Completează numele tehnicianului
3. Click "Adaugă"

### 2. Evaluare Tehnician
1. Mergi la tab-ul "Evaluare"
2. Selectează tehnicianul
3. Ajustează scorurile pentru fiecare KPI (1-100)
4. Vezi previzualizarea scorului și bonusului
5. Salvează evaluarea

### 3. Vizualizare Grafice
1. Mergi la tab-ul "📈 Grafice"
2. Selectează un tehnician pentru evoluția individuală
3. Vezi graficele de echipă în partea de jos

### 4. Export Date
1. În tab-ul "Dashboard", secțiunea "Evaluări Recente"
2. Click "📊 Export Excel" pentru fișier .xlsx
3. Click "📄 Export PDF" pentru raport PDF

## 🔧 Configurare Producție

### 1. Variables de Mediu Producție

**Backend (.env):**
env
MONGO_URL=mongodb://your-production-mongo-server:27017
DB_NAME=bonus_system_prod


**Frontend (.env):**
env
REACT_APP_BACKEND_URL=https://your-api-domain.com


### 2. Build Frontend pentru Producție

bash
cd frontend
yarn build


Fișierele optimizate vor fi în directorul build/.

### 3. Deployment Opțiuni

#### Docker
dockerfile
# Dockerfile pentru backend
FROM python:3.11
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["uvicorn", "server:app", "--host", "0.0.0.0", "--port", "8001"]


#### Nginx pentru Frontend
nginx
server {
    listen 80;
    server_name your-domain.com;
    
    location / {
        root /path/to/frontend/build;
        try_files $uri $uri/ /index.html;
    }
    
    location /api/ {
        proxy_pass http://localhost:8001;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}


## 🐛 Troubleshooting

### Probleme Comune

**1. Eroare conexiune MongoDB**
bash
# Verifică dacă MongoDB rulează
mongosh
# Sau
docker ps | grep mongo


**2. Port ocupat**
bash
# Verifică ce proces folosește portul
lsof -i :8001  # Backend
lsof -i :3000  # Frontend


**3. Dependențe lipsă**
bash
# Backend
pip install --upgrade pip
pip install -r requirements.txt

# Frontend
yarn install --force


## 📞 Suport

Pentru probleme sau întrebări:
1. Verifică secțiunea "Troubleshooting"
2. Consultă documentația API la http://localhost:8001/docs
3. Verifică log-urile aplicației

## 📄 Licență

Acest proiect este pentru uz intern al echipei tehnice.

---

**Sistem dezvoltat pentru echipa tehnică - Management eficient al bonificațiilor! 🚀**
