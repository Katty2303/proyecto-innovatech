# 🚀 Proyecto Semestral: Innovatech Chile

## 📋 Información del Grupo

- **Institución:** Duoc UC
- **Asignatura:** Introducción a Herramientas DevOps (ISY1101)
- **Integrantes:** Nicolás Lorca Salamanca - Katherine Ramírez Carvajal
- **Docente:** Miguel Acuña Narvaez
- **Sección:** 301V

---

## 🛠️ Arquitectura de la Solución

Este proyecto utiliza una arquitectura basada en **Microservicios** totalmente contenedorizados con Docker:

- **Frontend:** Aplicación optimizada mediante compilación Multi-Stage, servida de forma segura a través de un servidor Nginx con mínimos privilegios (usuario no-root).
- **Backend Ventas:** Microservicio desarrollado en Spring Boot (Java 17), configurado para operar en el puerto `8081`.
- **Backend Despachos:** Microservicio desarrollado en Spring Boot (Java 17), configurado para operar en el puerto `8082`.
- **Base de Datos:** Motor PostgreSQL centralizado conectado a través de una red puente aislada (`red-innovatech`).

---

## 🤖 Pipeline de Automatización (CI/CD)

La solución cuenta con un flujo continuo integrado en **GitHub Actions** que realiza las siguientes fases de forma automática ante cada cambio (`push`):

1. **Build & Test:** Descarga y compilación de dependencias.
2. **Docker Publish:** Construcción de imágenes de producción y publicación en Docker Hub de forma segura.
3. **CD (Despliegue Automático):** Conexión vía SSH con la instancia EC2 de AWS para descargar los nuevos contenedores mediante Docker Compose sin intervención manual.
