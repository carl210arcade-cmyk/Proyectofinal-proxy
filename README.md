
# Infraestructura del Proyecto

Este proyecto implementa una arquitectura basada en contenedores Docker para desplegar un entorno web con administración centralizada mediante un servidor **Reverse Proxy**, dos sitios HTML estáticos y el sistema ERP **Odoo** con base de datos PostgreSQL.

---

## Componentes del Entorno

| Servicio | Función | Tecnología | Puerto(s) |
|---------|---------|------------|-----------|
| **Reverse Proxy** | Administración de dominios, rutas y certificados | Nginx Proxy Manager | 80, 443, 81 |
| **Sitio Web Estático 1** | Página HTML genérica | Nginx (alpine) | Interno 80 |
| **Sitio Web Estático 2** | Página HTML genérica | Nginx (alpine) | Interno 80 |
| **Aplicación ERP** | Odoo 16 | Odoo (Python) | Interno 8069 |
| **Base de Datos** | Almacenamiento persistente | PostgreSQL 13 | Interno 5432 |

Todos los servicios se encuentran dentro de la red privada `proxy-net`, lo que permite comunicación interna segura.

---

## Cumplimiento de Requerimientos

### 1. Servidor Reverse Proxy (Nginx Proxy Manager)
- Se utiliza **Nginx Proxy Manager** para gestionar múltiples sitios.
- Redirige tráfico mediante reglas equivalentes a la directiva `proxy_pass`.
- Soporta habilitación de certificados SSL/TLS (HTTPS).
- Publicación activa en puertos:
  - **80 (HTTP)**
  - **443 (HTTPS)**

✅ Requisito cumplido.

---

### 2. Servidor Nginx + Base de Datos
- Se utilizaron dos servidores web mediante la imagen **nginx:alpine**.
- Se desplegaron sitios web HTML personalizados.
- Ambos sitios escuchan en el puerto interno 80 y son accedidos a través del reverse proxy.
- La base de datos se implementa con **PostgreSQL**, utilizada por Odoo.

✅ Requisito cumplido.

---

### 3. Servidor HTML Alternativo (Reemplazo de Apache2)
Originalmente se solicitaba Apache2; sin embargo, se utilizó **Nginx** debido a su rendimiento y simplicidad.

| Requisito original | Implementación equivalente |
|-------------------|---------------------------|
| Apache2 + HTML | Nginx + HTML |

El objetivo (publicar un sitio HTML en puerto 80) **se cumple correctamente** con Nginx.

✅ Requisito cumplido (con mejora tecnológica).

---

## Conclusión

Este proyecto cumple con los objetivos planteados al implementar un entorno modular, seguro y escalable basado en contenedores.  
El uso de **Nginx como reverse proxy** facilita la gestión centralizada del tráfico web y permite incorporar HTTPS mediante certificados SSL.  
Además, el despliegue de sitios HTML y la integración del ERP Odoo con PostgreSQL se realizó de manera limpia y organizada, optimizando la interacción entre servicios.

---
