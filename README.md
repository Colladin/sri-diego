# Documentacion de la tarea de la UT1
* **Alumno:** Diego Collado Gómez
* **Módulo:** SRI
* **Instituto:** IES Miguel Herrero Pereda

---

## 1. Esquema de la Arquitectura en AWS

* **VPC:** `vpc-diego` (`10.3.0.0/16`)
* **Subred pública:** `subnet-pub-diego` ("10.3.1.0/24")
* **Puerta de enlace de Internet (IGW):** "igw-diego"
* **Tabla de rutas:** `rt-pub-diego` (asociada al IGW para salida a Internet)
* **Grupo de seguridad:** `sg-web-diego` (con reglas de mínimo privilegio: SSH desde la IP de trabajo, HTTP en puertos 80 y 8080 abiertos al exterior)
* **Instancia EC2:** `web-diego` (tipo `t3.medium`, Ubuntu Server, asociada al par de claves `vockey`)

---

## 2. Instalación y Configuración Básica de Nginx

* **Qué se ha hecho:** Se instaló Nginx desde los repositorios de Ubuntu. Se configuró el sitio por defecto para servir una página personalizada con el nombre del autor y se habilitó la ruta `/estado`. Además, se investigó y aplicó la directiva para ocultar la versión de Nginx a nivel global (`http`), comprobando las cabeceras de respuesta antes y después
* **Cómo se ha comprobado:** Reiniciando el servicio y comprobando su arranque automático tras reiniciar la instancia, y validando las cabeceras HTTP mediante `curl`.

---

## 3. Sitios Virtuales

* **Qué se ha hecho:** Se configuraron tres sitios web independientes con sus respectivas carpetas en `/var/www/` y ficheros de configuración en `sites-available/`:
  1. `www.diego.test` (y su alias `diego.test`) respondiendo en el puerto 80.
  2. `blog.diego.test` respondiendo en el puerto 80.
  3. Intranet corporativa respondiendo en el puerto 8080.
  4. Sitio por defecto para peticiones huérfanas o por IP.
* **Cómo se ha comprobado:** Modificando el fichero `hosts` del equipo local y comprobando el acceso mediante navegador a cada uno de los dominios y al puerto 8080.

---

## 4. Ampliación de Nginx con Módulos

* **Qué se ha hecho:** Se instaló y configuró el módulo `fancyindex` para listar el contenido de la carpeta `/descargas/` con formato de tamaño legible y hora local de Madrid. Asimismo, se integró Nginx con PHP-FPM para procesar la página `hora.php` configurando explícitamente la zona horaria de Madrid.
* **Tabla de módulos utilizados:**

| Módulo | Descripción / Utilidad | Origen | Bloque de activación |
| :--- | :--- | :--- | :--- |
| `ngx_http_core_module` | Gestión básica de peticiones y directorios | De serie | `http` / `server` |
| `ngx_http_fancyindex_module` | Listado avanzado y personalizable de directorios | Externo (instalado) | `location` |
| `ngx_http_fastcgi_module` | Conexión con servidores FastCGI (PHP-FPM) | De serie | `location ~ \.php$` |

---

## 5. Autenticación y Control de Acceso

* **Qué se ha hecho:** Se protegió la Intranet completa (puerto 8080) requiriendo autenticación mediante ficheros externos de credenciales (`.htpasswd_intranet`) para los usuarios `diego` e `profesor`. Para la ruta `/admin/` del sitio `www.diego.test`, se configuró un acceso híbrido (`satisfy any`) que permite la entrada libre sin contraseña desde `127.0.0.1` y la IP de trabajo permitida, exigiendo obligatoriamente autenticación exclusiva con el usuario `diego` (restringiendo al usuario `profesor`) desde cualquier otra red externa.
* **Cómo se ha comprobado:** Realizando peticiones y pruebas de acceso tanto desde la red local como desde una red externa.
