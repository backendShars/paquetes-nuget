# Descripción de librerías NuGet usadas en Backend .NET

| Paquete                                       | Funcionalidad                                                                                                                  | Uso común en Backend           |
|-----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|-------------------------------|
| **BCrypt.Net-Next/4.0.3**                     | Encriptación y verificación segura de contraseñas usando bcrypt.                                                               | Seguridad para contraseñas     |
| **Cortex.Mediator/2.1.0**                     | Implementa el patrón Mediator (CQRS), separa comandos/queries y handlers para evitar acoplamiento directo.                     | Lógica desacoplada, CQRS      |
| **EntityFrameworkCore.CreatedUpdatedDate/8.0.0** | Permite agregar automáticamente fechas de creación/modificación a entidades en EF Core.                                        | Auditoría, seguimiento        |
| **Humanizer/2.14.1**                          | Proporciona utilidades para mostrar datos legibles (fechas, números, etc.) y transformar cadenas a formato humano.            | UX/Presentación de datos      |
| **Microsoft.AspNetCore.Authentication.JwtBearer/9.0.10** | Implementa seguridad JWT para ASP.NET Core.                                                                                   | Autenticación con tokens      |
| **Microsoft.EntityFrameworkCore.Relational.Design/1.1.6** | Herramientas para diseño y migración de modelos relacionales.                                                                | Modelado y migraciones        |
| **Microsoft.EntityFrameworkCore.Relational/9.0.10** | Extiende EF Core para trabajar con bases de datos relacionales (joins, transacciones, etc).                                  | Persitencia avanzada SQL      |
| **Microsoft.EntityFrameworkCore/9.0.10**      | ORM principal para mapeo relacional, LINQ y migraciones.                                                                      | Acceso y gestión de datos     |
| **Microsoft.Extensions.DependencyInjection/9.0.10** | Inyección de dependencias para servicios, repositorios, etc.                                                                 | Configuración modular         |
| **Microsoft.IdentityModel.Tokens/8.14.0**     | Validación y manejo de tokens JWT y otros.                                                                                    | Seguridad en autenticación    |
| **MySql.EntityFrameworkCore/9.0.9**           | Proveedor EF Core para bases MySQL y MariaDB, con compatibilidad LINQ y migraciones.                                          | Acceso a MySQL                |
| **Swashbuckle.AspNetCore.Annotations/9.0.6**  | Permite usar anotaciones para personalizar endpoints en Swagger/OpenAPI.                                                      | Documentar la API             |
| **Swashbuckle.AspNetCore/9.0.6**              | Integra Swagger/OpenAPI para expone y testear APIs REST con UI interactiva.                                                   | Documentación automática      |
| **System.IdentityModel.Tokens.Jwt/8.14.0**    | Manejo avanzado de tokens JWT: emisión, firmado, validación y parseo.                                                         | Seguridad y autorización      |


## IAM vs Profile en DDD

En proyectos como **learning-center-platform-master**, los módulos **IAM** y **Profile** se implementan como *bounded contexts* completamente separados siguiendo DDD. No existe relación directa en dominio o tablas para garantizar independencia y claridad de responsabilidades.

---

### Definición de Contextos

- **IAM (Identity & Access Management):**
  - Gestiona credenciales, autenticación y autorización.
  - Incluye usuario, contraseña (hash), login/JWT, permisos y seguridad.

- **Profile:**
  - Gestiona la información de usuario extendida.
  - Contiene nombre, datos personales, dirección de contacto, preferencias, etc.

---

### ¿Por qué ambos manejan “usuarios”?

Aunque ambos manejan “usuarios”, cumplen **roles distintos**:
- [translate:Un usuario registrado suele tener:]
  - Un registro en IAM (para autenticación y permisos).
  - Un perfil en Profile (para datos personales o sociales).

---

## ¿Qué es una ACL (Anti-Corruption Layer) en este contexto?

En DDD, una **ACL (Anti-Corruption Layer)** es una capa o patrón que aísla el dominio ante dependencias externas o diferencias de modelo (por ejemplo, entre dos contexts con diferentes formas de manejar usuarios).

---

### ¿Cómo actúa una ACL entre IAM y Profile?

- IAM y Profile siguen modelos y reglas independientes.
- Si Profile necesita interactuar o consultar datos de IAM, **evita depender directamente de sus detalles internos** o realizar acoplamientos fuertes.
- La ACL actúa como fachada e intermediario: traduce, adapta y aísla la comunicación para que ambos contextos puedan evolucionar de manera segura y sin “contaminar” sus modelos internos.

#### Ejemplo

Si desde Profile se quiere validar autenticación de IAM:
- **Se crea una ACL (servicio, façade, adaptador)** que recibe peticiones, las transforma y traduce resultados.
- Profile *nunca depende del modelo interno* de IAM, sólo de la interfaz pública de la ACL.
- Si IAM cambia su modelo, la ACL lo adapta y Profile sigue ajeno a esos cambios.

---

### Ventajas principales

- **Aislamiento:** Cada contexto evoluciona y escala a su propio ritmo.
- **Flexibilidad:** Permite mapear y reconciliar diferencias de reglas y modelos.
- **Protección:** Evita dependencias cruzadas y contaminación de modelos.

---

## En resumen

- En DDD, **una ACL NO es una lista de control de acceso de redes**, sino una *Anti-Corruption Layer*.
- Es ideal cuando tienes contextos que gestionan conceptos similares pero requieren reglas distintas (como IAM y Profile).
- Facilita integración y colaboración sin acoplar ni corromper los modelos internos, asegurando **escalabilidad y mantenibilidad real** en el tiempo.
