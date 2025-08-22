# Instalación y Configuración de Nexus Local

---

Este repositorio explica cómo instalar y configurar un **Nexus Repository Manager** local para almacenar imágenes Docker, y cómo usarlo para **crear tags, subir y descargar imágenes**.

---

## 1. Instalación de Nexus

1. Clonar este repositorio o crear una carpeta local para Nexus:

```bash
git clone https://github.com/TANHEHANZ/nexus.git
cd nexus
```

---

## 2. Levantar Nexus

```bash
docker-compose -f docker-compose-nexus.yml up -d
```

---

## 3. Consultar password por defecto

Para obtener la contraseña inicial del usuario `admin`:

```bash
docker exec -it <nombre-del-contenedor> cat /nexus-data/admin.password
```

> Reemplaza `<nombre-del-contenedor>` por el nombre real del contenedor de Nexus, por ejemplo `nexus`.

---

## 4. Acceder a la interfaz web

Visitar:

```
http://localhost:8081
```

Cambiar la contraseña del usuario `admin` según se indique al iniciar.

---

## 5. Uso de Nexus con Docker

Se recomienda leer los documentos específicos para cada operación:

- **[Creación de tags](./creacion-tags.md)** → Cómo taguear imágenes locales para tu registry.
- **[Listado de imágenes](./listado-imagenes.md)** → Cómo ver qué imágenes están en Nexus.
- **[Push de imágenes](./push-imagenes.md)** → Cómo subir imágenes locales a Nexus.
- **[Pull de imágenes](./pull-imagenes.md)** → Cómo descargar imágenes desde Nexus.
