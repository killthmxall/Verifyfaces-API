
# 📁 Gestión de Galerías e Imágenes con API y PowerShell

---

## 🖥️ Obtener listado de nombres de archivos (PowerShell)

El siguiente comando lista los nombres de archivos en el directorio actual, excluyendo el archivo `lista_imagenes.txt`, ordenándolos por el número inicial del nombre de archivo y guardando el resultado en `lista_imagenes_numeros.txt`.

```powershell
Get-ChildItem -File |
  Where-Object { $_.Name -ne 'lista_imagenes.txt' } |
  Sort-Object { [int]($_.Name.Split('-')[0]) } |
  Select-Object -ExpandProperty Name >
  lista_imagenes_numeros.txt
```

---

## 🌐 API VerifyFaces

### 🔍 Obtener imágenes de una galería

**Endpoint:**

```
GET /companies/{company}/galleries/{gallery}
```

**Descripción:**

Obtiene la lista de imágenes dentro de una galería para la empresa especificada.

**Parámetros de ruta:**

- `company`: ID de la empresa (number)
- `gallery`: ID de la galería (number)

**Parámetros de query:**

- `perPage`: número de resultados por página (opcional)
- `page`: número de página (opcional)

**Ejemplo con Curl:**

```bash
curl -X 'GET'   'https://dashboard-api.verifyfaces.com/companies/54/galleries/466?perPage=100&page=1'   -H 'accept: application/json'   -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjE4NCwiaWF0IjoxNzQ2NzE3NTkxLCJleHAiOjE3NDY3MjExOTF9.s8I90pfl0Kyg32T1c9olxPBDcFIz05P2B7x0gHDCS5I'
```

---

### 📤 Subir imágenes a una galería

**Endpoint:**

```
POST /companies/{company}/galleries/{gallery}/upload
```

**Descripción:**

Carga una o más imágenes en la galería de la empresa especificada.

**Parámetros de ruta:**

- `company`: ID de la empresa (number)
- `gallery`: ID de la galería (number)

**Cuerpo de la petición (multipart/form-data):**

- `images`: array de archivos de imagen (obligatorio)
- `metadata`: array de objetos con información adicional (opcional)

**Ejemplo con Curl:**

```bash
curl -X 'POST'   'https://dashboard-api.verifyfaces.com/companies/54/galleries/466/upload'   -H 'accept: application/json'   -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjE4NCwiaWF0IjoxNzQ2NzE3NTkxLCJleHAiOjE3NDY3MjExOTF9.s8I90pfl0Kyg32T1c9olxPBDcFIz05P2B7x0gHDCS5I'   -H 'Content-Type: multipart/form-data'   -F 'images=@51-0103846432-MemNo 982.png;type=image/png'
```


---

### ✏️ Actualizar metadata de una imagen

**Endpoint:**

```
PATCH /companies/{company}/galleries/{gallery}/{image}
```

**Descripción:**

Actualiza los metadatos de una imagen específica dentro de una galería.

**Parámetros de ruta:**

- `company`: ID de la empresa (number)
- `gallery`: ID de la galería (number)
- `image`: ID de la imagen (number)

**Cuerpo de la petición (application/json):**

```json
{
  "metadata": {
    "name": "0100019041-MemNo 392",
    "comment": "string"
  }
}
```

**Ejemplo con Curl:**

```bash
curl -X 'PATCH'   'https://dashboard-api.verifyfaces.com/companies/54/galleries/466/104877'   -H 'accept: application/json'   -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjE4NCwiaWF0IjoxNzQ2NzE3NTkxLCJleHAiOjE3NDY3MjExOTF9.s8I90pfl0Kyg32T1c9olxPBDcFIz05P2B7x0gHDCS5I'   -H 'Content-Type: application/json'   -d '{"metadata":{"name":"0103837951-MemNo 961","comment":""}}'
```


---

## 🔐 Autenticación

Ambos endpoints requieren autenticación mediante token Bearer JWT:

```http
Authorization: Bearer <tu_token_de_acceso>
```

Reemplaza `<tu_token_de_acceso>` con un token válido generado por el sistema.

---
