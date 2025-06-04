# Proyecto n8n con RAG y Supabase

**Diana Marcela Salguero Sánchez**  
**Programación III**  
**Universidad Tecnológica de Pereira**  
**Semestre 2025-1**

---

## Especificaciones del Computador

- **Procesador:** AMD Ryzen 5 4500U con Radeon Graphics (2.38 GHz)  
- **RAM:** 8 GB  
- **Sistema Operativo:** Windows 11 Home  

## Especificaciones Máquina Virtual

- **Nombre:** n8n proyecto  
- **Sistema Operativo:** Ubuntu 64-bit  
- **Memoria Base:** 2048 MB  
- **Memoria de Video:** 16 MB  

---

## Objetivo del Proyecto

Implementar un agente de IA con RAG utilizando n8n y Supabase para almacenar la memoria de las conversaciones, y utilizar una base de datos vectorial que permita digerir documentos, generando respuestas claras y precisas.

---

## ¿Qué es un RAG en n8n?

**RAG (Retrieval-Augmented Generation)** es una técnica en la que el modelo de lenguaje primero busca información externa antes de generar una respuesta.  
Implementarlo en n8n permite:

1. Automatizar respuestas inteligentes con datos personalizados.  
2. Asegurar privacidad y control total sobre los datos.  
3. Crear asistentes personalizados conectados a servicios como WhatsApp, Google Drive o Telegram.

---

## Proceso de Instalación

1. Instalar **VirtualBox** y **Ubuntu Server LTS 24**.  
2. Activar **Docker Compose** durante la instalación.  
3. Crear una carpeta para el proyecto y dentro, un archivo `docker-compose.yml` con el siguiente contenido:

```yaml
version: '3.8'
services:
  n8n:
    image: n8nio/n8n
    restart: always
    ports:
      - "5678:5678"
    volumes:
      - n8n_data:/home/node/.n8n
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=# user
      - N8N_BASIC_AUTH_PASSWORD=# Password
    user: node
    networks:
      - n8n_network

  ollama:
    image: ollama/ollama
    container_name: ollama
    restart: unless-stopped
    ports:
      - "11434:11434"
    volumes:
      - ./ollama_data:/root/.ollama
    networks:
      - n8n_network

volumes:
  n8n_data:

networks:
  n8n_network:
    driver: bridge
