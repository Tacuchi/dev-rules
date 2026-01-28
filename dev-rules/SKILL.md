---
name: dev-rules
description: >
  Reglas de desarrollo globales para todos los proyectos. Activar siempre que Claude
  asista en tareas de programación, revisión de código, generación de código, commits,
  pull requests o cualquier tarea de ingeniería de software. Define idioma de comunicación,
  estilo de código, convenciones de git, principios de arquitectura, seguridad, rendimiento
  y manejo de errores. Aplica a cualquier lenguaje o framework.
---

# Dev Rules

## Idioma y Comunicación
- Responder siempre en español.
- Ser conciso pero completo.
- No disculparse por errores; corregirlos directamente.

## Formato y Estilo
- Seguir las convenciones del proyecto existente.
- Nombres descriptivos; el código debe hablar por sí mismo.
- Preferir código conciso sobre código documentado verbosamente.

## Documentación
- Documentar solo decisiones técnicas importantes o lógica no obvia.
- Comentarios solo para explicar el "por qué", nunca el "qué".
- Usar `TODO` para código incompleto.

## Git y Control de Versiones
- No hacer commit ni push sin confirmación explícita del usuario.
- Conventional Commits: `feat:`, `fix:`, `docs:`, `chore:`, `refactor:`, `test:`, `ci:`.
- Ramas descriptivas: `feature/`, `fix/`, `hotfix/`, `chore/`.

## Código Limpio
- Principios SOLID.
- Composición sobre herencia.
- Sin comentarios decorativos ni separadores visuales excesivos (`====`, `----`, checks).
- Early returns para condiciones de error (evitar nesting profundo).
- Métodos/funciones pequeños con una sola responsabilidad.
- DRY: extraer lógica duplicada solo cuando se repite 3+ veces.

## Arquitectura y Patrones
- Respetar la arquitectura existente del proyecto (microservicios, monolito, etc.).
- Separar claramente capas: controlador, servicio, repositorio/data.
- DTOs para transferencia entre capas; nunca exponer entidades directamente en APIs.
- Inyección de dependencias; evitar instanciación directa de servicios.

## TypeScript/Angular
- Evitar `any`; usar tipos específicos o `unknown`.
- `inject()` para inyección de servicios.
- `async` pipe para observables en templates.
- Preferir standalone components y signals.

## Java/Spring Boot
- Constructor Injection (sin Field Injection en producción).
- `@Transactional(readOnly = true)` para lecturas, `@Transactional` para escrituras.
- Java records para DTOs Request/Response.
- Validar inputs con Jakarta Validation.

## Flutter/Dart
- Constructores `const` para widgets inmutables.
- Evitar `!` a menos que el valor esté garantizado no-nulo.
- Trailing commas para mejor formateo.
- State management (Bloc/Riverpod) para apps complejas.

## Kotlin/Compose
- Funciones `@Composable` en PascalCase como sustantivos.
- Parámetros: obligatorios primero, luego `Modifier`, luego opcionales.
- `Modifier` se aplica solo al layout raíz.

## Performance
- Considerar el impacto en rendimiento de cada cambio.
- Usar caché cuando sea apropiado.
- Lazy loading y paginación; evitar cargar datos innecesarios.

## Manejo de Errores
- Fail fast: manejar errores al inicio de funciones.
- Logear con nivel apropiado: `ERROR`, `WARN`, `INFO`, `DEBUG`.
- Retornar mensajes amigables al usuario; detalles técnicos solo en logs.

## Seguridad
- Nunca exponer secrets, API keys o credenciales en código o logs.
- Nunca logear datos sensibles (passwords, tokens, datos personales).
- Parametrizar siempre queries SQL.
- Validar y sanitizar toda entrada externa.

## Testing
- No generar código de pruebas a menos que se solicite explícitamente.

## Docker y Despliegue
- No modificar Dockerfiles ni pipelines CI/CD sin confirmación explícita.
- Respetar la separación de entornos (dev, cert, prod).

## Base de Datos
- Nunca ejecutar queries destructivas (DROP, TRUNCATE, DELETE masivo) sin confirmación.
- Preferir migraciones versionadas sobre cambios manuales de esquema.
