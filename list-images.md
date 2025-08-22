    # Listado de Imágenes en Nexus

---

Este documento explica cómo consultar y listar las imágenes Docker que se encuentran en tu **Nexus Repository Manager** local.

---

## 1. Listar imágenes locales en Docker

Antes de consultar Nexus, puedes verificar tus imágenes locales:

```bash
docker images
```

Esto mostrará algo como:

```
REPOSITORY          TAG       IMAGE ID       CREATED        SIZE
mi-app              latest    abc123def456   2 days ago     150MB
```

---

## 2. Listar imágenes en Nexus

Para listar las imágenes almacenadas en tu repositorio de Nexus, puedes usar:

### a) Con `docker`

```bash
docker login <host-nexus>:<puerto>
docker pull <host-nexus>:<puerto>/<nombre-repositorio>/<imagen>:<tag>
```

Aunque `docker pull` es principalmente para descargar, si falla te indicará que la imagen no existe.

### b) Desde la interfaz web

1. Ingresa a la interfaz web de Nexus: `http://localhost:8081`.
2. Navega a **Browse** → **Repositories** → selecciona tu repositorio Docker.
3. Aquí podrás ver todas las imágenes y tags almacenados.

---

## 3. Recomendación

Para automatizar la consulta de imágenes y tags desde la línea de comandos, puedes usar la **API REST de Nexus**, ejemplo:

```bash
curl -u admin:<password> -X GET 'http://localhost:8081/service/rest/v1/components?repository=<nombre-repositorio>'
```

Esto listará los componentes (imágenes y tags) disponibles en el repositorio.

---

## 4. Siguientes pasos

Después de listar las imágenes, puedes:

- **[Push de imágenes](./push-imagenes.md)** → Subir nuevas imágenes a Nexus.
- **[Pull de imágenes](./pull-imagenes.md)** → Descargar imágenes desde Nexus.
