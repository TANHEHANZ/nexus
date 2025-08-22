# Push de Imágenes a Nexus

---

Este documento explica cómo subir imágenes Docker a tu **Nexus Repository Manager** local después de haber creado los tags correspondientes.

---

## 1. Iniciar sesión en Nexus

Antes de subir cualquier imagen, debes autenticarte en tu Nexus local:

```bash
docker login <host-nexus>:<puerto>
```

Por ejemplo:

```bash
docker login localhost:8082
```

Introduce tu usuario (`admin`) y la contraseña que consultaste previamente.

---

## 2. Subir una imagen con tag

Usa el comando `docker push` para subir la imagen etiquetada:

```bash
docker push <host-nexus>:<puerto>/<nombre-repositorio>/<imagen>:<tag>
```

Ejemplo:

```bash
docker push localhost:8082/docker-repo/mi-app:1.0.0
```

Esto subirá la imagen `mi-app` con el tag `1.0.0` al repositorio `docker-repo` en tu Nexus local.

---

## 3. Verificar subida

Después de hacer push, puedes verificar que la imagen se encuentra en Nexus:

- Desde la **interfaz web**: `http://localhost:8081` → **Browse** → tu repositorio Docker.
- Usando la **API REST** de Nexus:

```bash
curl -u admin:<password> -X GET 'http://localhost:8081/service/rest/v1/components?repository=<nombre-repositorio>'
```

---

## 4. Siguientes pasos

Después de subir la imagen, puedes:

- **[Pull de imágenes](./pull-imagenes.md)** → Descargar imágenes desde Nexus para probarlas o desplegarlas.
