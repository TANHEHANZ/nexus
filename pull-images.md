# Pull de Imágenes desde Nexus

---

Este documento explica cómo descargar imágenes Docker desde tu **Nexus Repository Manager** local después de haberlas subido o creado.

---

## 1. Iniciar sesión en Nexus

Antes de descargar cualquier imagen, debes autenticarte en tu Nexus local:

```bash
docker login <host-nexus>:<puerto>
```

Ejemplo:

```bash
docker login localhost:8082
```

Introduce tu usuario (`admin`) y la contraseña que consultaste previamente.

---

## 2. Descargar una imagen con tag

Usa el comando `docker pull` para traer la imagen desde Nexus:

```bash
docker pull <host-nexus>:<puerto>/<nombre-repositorio>/<imagen>:<tag>
```

Ejemplo:

```bash
docker pull localhost:8082/docker-repo/mi-app:1.0.0
```

Esto descargará la imagen `mi-app` con el tag `1.0.0` a tu máquina local.

---

## 3. Verificar descarga

Para verificar que la imagen se descargó correctamente:

```bash
docker images
```

Deberías ver algo como:

```
REPOSITORY                                TAG       IMAGE ID       CREATED        SIZE
localhost:8082/docker-repo/mi-app         1.0.0     abc123def456   2 days ago     150MB
```

---

## 4. Siguientes pasos

Después de descargar la imagen, puedes:

- Usarla para crear contenedores:

```bash
docker run -d --name mi-app-container localhost:8082/docker-repo/mi-app:1.0.0
```

- Verificar que funcione correctamente con tu aplicación.
