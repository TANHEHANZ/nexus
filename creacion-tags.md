# Creación de Tags en Nexus

---

Este documento explica cómo crear tags para imágenes Docker y subirlas a tu **Nexus Repository Manager** local.

---

## 1. Listar imágenes locales

Primero, verifica qué imágenes Docker tienes disponibles localmente:

```bash
docker images
```

Esto mostrará algo como:

```
REPOSITORY          TAG       IMAGE ID       CREATED        SIZE
mi-app              latest    abc123def456   2 days ago     150MB
```

---

## 2. Crear un tag para una imagen

Para etiquetar (tag) una imagen y prepararla para subirla a Nexus:

```bash
docker tag <imagen-local>:<tag> <host-nexus>:<puerto>/<nombre-repositorio>/<imagen>:<tag>
```

Ejemplo:

```bash
docker tag mi-app:latest localhost:8082/docker-repo/mi-app:1.0.0
```

> Aquí:
>
> - `<host-nexus>:<puerto>` es tu Nexus local, normalmente `localhost:8082`.
> - `<nombre-repositorio>` es el repositorio Docker que creaste en Nexus.
> - `<imagen>:<tag>` es el nombre y versión de la imagen.

---

## 3. Verificar el tag

Para asegurarte de que el tag se aplicó correctamente:

```bash
docker images
```

Deberías ver algo como:

```
REPOSITORY                                TAG       IMAGE ID       CREATED        SIZE
localhost:8082/docker-repo/mi-app         1.0.0     abc123def456   2 days ago     150MB
mi-app                                     latest    abc123def456   2 days ago     150MB
```

---

## 4. Siguientes pasos

Después de crear el tag, puedes seguir con los siguientes documentos para:

- **[Push de imágenes](./push-imagenes.md)** → Subir la imagen etiquetada a Nexus.
- **[Pull de imágenes](./pull-imagenes.md)** → Descargar imágenes desde Nexus.
