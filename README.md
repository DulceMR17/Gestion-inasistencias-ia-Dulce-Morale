#  Sistema Automatizado de Gestión de Inasistencias con IA y Telegram

Este proyecto consiste en un sistema de flujo de trabajo automatizado diseñado en **n8n** y desplegado sobre **Docker**. Su objetivo principal es optimizar, analizar mediante Inteligencia Artificial y gestionar el control de justificaciones de inasistencias de estudiantes, permitiendo consultas en tiempo real a través de un **Bot de Telegram**.

---

## Características Principales

* **Interconexión con Telegram:** Los usuarios interactúan directamente con un Bot enviando un ID de solicitud único de 4 dígitos.
* **Procesamiento de Datos dinámico:** Integración con **Google Sheets** para la lectura y actualización inmediata de la base de datos de inasistencias.
* **Análisis con Inteligencia Artificial:** Flujos preparados para la clasificación inteligente de motivos de faltas y comprobantes médicos adjuntos.
* **Túnel Seguro de Conexión:** Configuración integrada con **Ngrok** para habilitar Webhooks bajo protocolos seguros (`https://`) requeridos por la API de Telegram.
* **Infraestructura Contenerizada:** Despliegue rápido, limpio y portable utilizando **Docker** y **Docker Compose**.

---

##  Tecnologías Utilizadas

* **n8n** (Orquestador de Automatización y Workflow)
* **Docker & Docker Compose** (Contenerización de Entornos)
* **Ngrok** (Túnel de Red seguro para Webhooks)
* **Google Sheets API** (Base de Datos / Almacenamiento)
* **Telegram Bot API** (Interfaz de usuario)

---

##  Estructura del Proyecto de Contenedores

El entorno de ejecución local está definido mediante el archivo `docker-compose.yml`, el cual configura las variables de entorno necesarias para la persistencia de datos y la zona horaria correcta:

```yaml
version: '3.8'

services:
  n8n:
    image: docker.n8n.io/n8nio/n8n
    restart: always
    ports:
      - "5678:5678"
    environment:
      - N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true
      - TZ=America/Guatemala_City
      - WEBHOOK_URL=https://TU_SUBDOMINIO.ngrok-free.dev/
    volumes:
      - n8n_data:/home/node/.n8n

volumes:
  n8n_data:
