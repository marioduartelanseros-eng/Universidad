# Entra en el parcial
**Requisitos funcionales/no funcionales**
**diagramas de secuencia**
**diagramas de arquitectura**
**Casos de uso** (Seguir plantilla pagina 19 bloque 3)

## Apuntes permitidos(impresos, escritos, etc)
# Ejercicios - Bloque 3

3.1 Clasifica los siguientes requisitos de una aplicación de gestión de clases para profesores como funcionales, no funcionales o ninguno de los dos:  
1. Registro de estudiantes  - Funcional
2. La aplicación debe seguir el patrón MVC - Nada
3. Registro de asistencia de los estudiantes  - Funcional 
4. Todos los profesores de la universidad deben poder hacer uso de la aplicación al mismo tiempo - No funcional (Reliability Req)
5. Creación y asignación de tareas y proyectos - funcional
6. Enviar mensajes a los estudiantes  - funcional
7. Los datos de los estudiantes deben estar cifrados  - no funcional (safety requirements)
8. Cada operación debe realizarse en menos de un segundo  - no funcional (Efficiency Requirments)
9. El diseño estético debe ser atractivo  - ninguno (no es un requisito porque no quiere decir nada, es subjetivo)
10. La aplicación debe estar disponible las 24 horas los 7 días de la semana  - no funcional (Reliability Req)
11. Programación de horarios de clase - Funcional


3.2 Desarrolla el siguiente requisito “Búsqueda por nombre de un aula para programar una clase en un campus dado”. como 
1) caso de uso y como 
Nombre: R1 (Nombre es solo un identificador no descripcion)
- Actor: Profesor
- Descripcion: Busqueda de aula
- Precondiciones:aulas registrada en el sistema, profesor registrado en la app
- Dependencias: no podemos ponerlo porque solo tenemos un requisito
- Escenario:1 ir a la pagina de busqueda, 2 introducir el termino de busqueda, 3 hacer la busqueda, 4 mostrar listado de aula, 
- Excepciones: ir a la pagina de busqueda, Informar al usuario 2.introduccion nombre aula, aula no encontrada
1) historias de usuario.  

Ejercicio 3.6  
Clasifica los siguientes requisitos no funcionales en su correspondiente subcategoría:  
2. La aplicación debe funcionar en Windows, Unix, MacOs, Android e iOS   (Portability Req)
3. La aplicación debe usar lenguaje inclusivo  (Ethical Req)
4. La aplicación debe estar disponible de lunes a viernes de 8h a 18h (Reliability)
5. La operación de registro debe realizarse en menos de 1 segundo (Performance)
6. La versión móvil de la aplicación debe ocupar menos de 100MB  
7. La aplicación debe ser compatible con el sistema de videoconferencia Zoom  (interoperabilidad)
8. Se deben entregar tanto los ejecutables de las diferentes versiones como el código fuente  (Delivery)
9. La aplicación debe ser accesible para personas con discapacidades visuales o motoras (usability)

Ejercicio 3.10  
Crea un diagrama de secuencia para seleccionar un producto del catálogo y añadirlo al carro de la  
compra teniendo en cuenta el diagrama de arquitectura del ejercicio 3.7
