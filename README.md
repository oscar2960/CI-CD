# Proyecto Docker + Jenkins + Flask + MySQL

## 📌 Descripción
Este proyecto contiene:
- Una aplicación Flask dentro de un contenedor Docker.
- Una base de datos MySQL en un segundo contenedor.
- Ambos contenedores se comunican mediante Docker Compose.
- Un `Jenkinsfile` que permite que Jenkins construya y despliegue automáticamente los contenedores.
- Preparado para integrarse con GitHub mediante **webhooks** para CI/CD.

---

## 🚀 Instrucciones de uso

### 1. Clonar el repositorio
```bash
git clone https://github.com/TU_USUARIO/TU_REPO.git
cd TU_REPO
```

---

## 🐳 2. Construir y ejecutar los contenedores con Docker Compose

```bash
docker-compose build
docker-compose up -d
```

La aplicación Flask quedará disponible en:

```
http://localhost:5000
```

---

## 🔧 3. Configurar Jenkins para CI/CD

### ✔ Paso 1: Crear un Job Pipeline
Dentro de Jenkins:
1. Nuevo Job → **Pipeline**
2. Activar "GitHub Project" → colocar URL del repo.
3. En "Pipeline from SCM":
   - SCM: **Git**
   - URL: `https://github.com/TU_USUARIO/TU_REPO.git`
   - Script path: `Jenkinsfile`

---

## 🔔 4. Activar Webhooks desde GitHub hacia Jenkins

### ✔ Paso 1: Obtener la URL del webhook
Si Jenkins está local, debes exponerlo con **ngrok**:

```bash
ngrok http 8080
```

Obtendrás una URL como:

```
https://abcd1234.ngrok.io
```

El webhook debe apuntar a:

```
https://TU_URL_JENKINS/github-webhook/
```

Ejemplo:
```
https://abcd1234.ngrok.io/github-webhook/
```

---

## ✔ Paso 2: Crear webhook en GitHub
En GitHub:
1. Settings → Webhooks → Add webhook  
2. **Payload URL:**  
   ```
   https://TU_URL_JENKINS/github-webhook/
   ```
3. **Content-type:** `application/json`
4. **Trigger:**  
   ✓ Just the push event  
5. Guardar

---

## ♻ ¿Qué ocurrirá ahora?
Cada vez que hagas:

```bash
git add .
git commit -m "update"
git push
```

GitHub enviará el evento a Jenkins → Jenkins ejecutará:
- Checkout del código  
- Build de contenedores  
- Deploy automático  

---

## 📁 Estructura del proyecto

```
/
├── app.py
├── Dockerfile
├── docker-compose.yml
├── Jenkinsfile
├── requirements.txt
└── README.md
```

---

## ✨ Listo
Tu flujo CI/CD con Docker + Jenkins + GitHub está completamente operativo.
