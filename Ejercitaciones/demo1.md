## Ejercicio para realizar en clase

#### Descripción del requerimiento

Se desea agregar la persona de contacto del club. El tipo de dato es un texto, es obligatorio y no puede ser ni NULL ni acío.                                                                                       El El cambio debe mantener retro-compatibilidad con los clientes actuales que consumen la API, siguiendo un ciclo completo de versionado y deprecación.

##### Pasos a seguir

###### Parte 1 — Cambio de modelo, migración y Endpoint v1 (retro-compatible)

1. Crear la property ContactName en la entidad Club (en Entities/Entities/Club.cs).
2. Configurar EntityFramework en Repository/ApplicationDbContextConfig.cs para que la columna sea NOT
NULL.
3. Generar la migración de modo que los clubes existentes reciban el valor temporal "nombre temporal"
(usar defaultValue en la columna nueva para cubrir las filas ya cargadas).
4. En el endpoint actual POST /club, no exponer ContactName en el ClubDTO público (v1). El valor por
defecto "nombre temporal" se asigna del lado servidor (en el use case o el mapper), no desde el cliente.
6. Marcar el endpoint como 'obsoleto' con fecha de eliminación prevista.
7. Agregar test de aceptación (Given_When_Then) verificando que un POST a /club sin ContactName sigue
funcionando y que el club queda persistido con "nombre temporal".
8. Commit: Mantener retro-compatibilidad en POST /club asignando ContactName por defecto

###### Parte 2 — Eliminar el valor por defecto de SQL

9. Se elimina el defaultvalue creado en el punto 3. Al haber creado el valor por defecto en el endpoint original, ya no es mas neccesario en la DB.

###### Parte 3 — Endpoint v2 con validación real

9. Crear ClubV2DTO con todos los campos de ClubDTO más ContactName marcado con [Required] y validación de
no-vacío (ej: [MinLength(1)] o validación custom para rechazar strings con solo espacios).
10. Crear el endpoint POST /club/v2 que reciba ClubV2DTO.
11. Agregar tests de aceptación:
    - Given ContactName válido → When POST /club/v2 → Then 200 OK.
    - Given ContactName vacío o null → When POST /club/v2 → Then 400 BadRequest.
12. Commit: Agregar POST /club/v2 con ContactName obligatorio

###### Parte 4 — Deprecación del endpoint viejo

15. Eliminar el endpoint POST /club y el ClubDTO v1 si ya no se usa en ningún otro lado.
16. Verificar que los tests de aceptación del v1 fueron removidos o adaptados.
17. Commit: Eliminar endpoint obsoleto POST /club