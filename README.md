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
