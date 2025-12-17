# M5_Brief_2:  Application Backend + Frontend – Publication Docker Hub

Ce projet contient deux services Docker :

- **Backend (FastAPI – uvicorn)**
- **Frontend (Streamlit)**

Les deux images sont automatiquement construites et publiées sur Docker Hub via GitHub Actions.

Chaque image est disponible sous deux tags :

- `latest` → version stable la plus récente
- `<SHA GitHub>` → commit précis pour traçabilité

---

## Images disponibles sur Docker Hub

| Composant | Image |
|----------|----------------|
| Backend  | `kaledtalbi/backend` |
| Frontend | `kaledtalbi/frontend` |



---

# Comment installer et lancer les images

## 1️ Installer Docker & Docker Compose

Linux / Windows / Mac → installer depuis :
https://docs.docker.com/get-docker/

---

## 2️ Pull des images ( Avec possibilité de faire communiquer backend/frontend)

Crée docker-compose.yml avec le contenu suivant : 
```bash
services:
  backend:
    image: kaledtalbi/backend:latest
    container_name: backend
    ports:
      - "8000:8000"

  frontend:
    image: kaledtalbi/frontend:latest
    container_name: frontend
    ports:
      - "8501:8501"
    depends_on:
      - backend
```
Puis :

```bash
docker compose up -d
```
L'application front est accessible à cet url: http://127.0.0.1:8501/

Si l'objectif est de tester le depoiment d'une image : 

### Backend

```bash
docker pull kaledtalbi/backend:latest
```

### Frontend

```bash
docker pull kaledtalbi/frontend:latest
```

---

## 43 Accéder aux services

###  Backend API
```
http://localhost:8000
```

Documentation OpenAPI :
```
http://localhost:8000/docs
```

###  Frontend Streamlit
```
http://localhost:8501
```

---

#  Images versionnées avec SHA

Chaque build reçoit un tag unique lié au commit Git :

Exemple :

```bash
docker pull kaledtalbi/backend:8d27c5e3b1d2
```

---

#  Mises à jour automatiques avec GitHub Actions

À chaque `git push` sur la branche `main` :

✔ build backend + frontend
✔ tag latest + SHA
✔ push sur Docker Hub
✔ cache Docker actif


